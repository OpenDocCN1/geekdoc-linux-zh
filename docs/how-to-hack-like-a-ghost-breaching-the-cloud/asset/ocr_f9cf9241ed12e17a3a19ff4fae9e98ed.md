| NODE | POD |
|---|---|
| ip-192-168-162-215.eu-... | api-core-deployment-d34c-7qxm |
| ip-192-168-12-123.eu-... | ssp-feeder-deployment-13fe-3evx |
| ip-192-168-89-110.eu-... | redis-depl-69dc-0vslf |
| ip-192-168-72-204.eu-... | audit-elastic-depl-3dbc-3qozx |

This rather explicit command only displays the spec.nodeName and metadata .name fields of the pods’ manifests. Let’s get some additional data, like secrets, service accounts, pod IPs, and so on. As you can see in Listing 8-4, the filter grows thicker to read, but it essentially walks through arrays and maps in YAML to fetch the relevant information.

```
shell> ./ kubectl get pods -o="custom-columns=\
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