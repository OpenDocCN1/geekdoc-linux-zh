
as which pods should run, which image they use, how they communicate with each other, and so on. Everything in Kubernetes revolves around that desired state. In fact, Kube’s main mission is to make that desired state a reality and keep it that way.

![](img/961e81aef23040d0fbe348f58c055860_130_0.png)

Figure 7-1: A pod composed of Nginx and Redis containers

In Listing 7-1, we create a manifest file that stamps the label app: myapp on a pod composed of two containers: an Nginx server listening on port 8080 and a Redis database available on port 6379. Here is the YAML syntax to describe this setup:

```
# myapp.yaml file
# Minimal description to start a pod with 2 containers
apiVersion: v1
kind: Pod  # We want to deploy a pod
metadata:
  name: myapp  # Name of the pod
  labels:
    app: myapp  # Label used to search/select the pod
spec:
  containers:
    - name: nginx   # First container
      image: sparcflow/nginx  # Name of the public image
      ports:
        - containerPort: 8080  # Listen on the pod's IP address
    - name: mydb    # Second container
      image: redis  # Name of the public image
      ports:
        - containerPort: 6379
```

Listing 7-1: The manifest file to create a pod comprising two containers

We send this manifest using the kubectl utility, which is the flagship program used to interact with a Kubernetes cluster. You'll need to download kubectl from https://kubernetes.io/docs/tasks/tools/install-kubectl/.

We update the kubectl config file ~/.kube/config to point to our cluster (more on that later) and then submit the manifest file in Listing 7-1:

```
root@DemLab:/# kubectl apply -f myapp.yaml

root@DemLab:/# kubectl get pods
```

| NAME | READY | STATUS | RESTARTS | AGE |
|------|-------|--------|----------|-----|
| myapp | 2/2 | Running | 0 | 1m23s |

Our pod consisting of two containers is now successfully running on one of the 100 machines in the cluster. Containers in the same pod are treated as a single unit, so Kube makes them share the same volume and network namespaces. The result is that our Nginx and database containers have the same IP address (10.0.2.3) picked from the network bridge IP pool (see “Resources” on page 119 for a pointer to more info on that) and can talk to each other using their namespace-isolated localhost (127.0.0.1) address, as depicted in Figure 7-2. Pretty handy.

> NOTE
Actually, Kubernetes spawns a third container inside the pod called the pause-container. This container owns the network and volume namespaces and shares them with the rest of the containers in the pod (refer to https://www.ianlewis.org/ for more on this).

![](img/961e81aef23040d0fbe348f58c055860_131_0.png)

![](img/961e81aef23040d0fbe348f58c055860_131_1.png)

Figure 7-2: Network configuration of the pod, containers, and the host machine (node)

Each pod has an IP address and lives on a virtual or bare-metal machine called a node. Each machine in our cluster is a node, so the cluster has 100 nodes. Each node hosts a Linux distribution with some special Kubernetes tools and programs to synchronize with the rest of the cluster.

One pod is great, but two are better, especially for resilience so the second can act as a backup should the first fail. What should we do? Submit the same manifest twice? Nah, we create a deployment object that can replicate pods, as depicted in Figure 7-3.

![](img/961e81aef23040d0fbe348f58c055860_132_0.png)

Figure 7-3: A Kube deployment object

A deployment describes how many pods should be running at any given time and oversees the replication strategy. It will automatically respawn pods if they go down, but its key feature is rolling updates. If we decide to update the container’s image, for instance, and thus submit an updated deployment manifest, it will strategically replace pods in a way that guarantees the continuous availability of the application during the update process. If anything goes wrong, the new deployment rolls back to the previous version of the desired state.

Let’s delete our previous stand-alone pod so we can re-create it as part of a deployment object instead:

```
root@DemoLab:/# kubectl delete -f myapp.yaml
```

To create the pod as a deployment object, we push a new manifest file of type Deployment, specify the labels of the containers to replicate, and append the previous pod’s configuration in its manifest file (see Listing 7-2). Pods are almost always created as part of deployment resources.

```
# deployment_myapp.yaml file
# Minimal description to start 2 pods
apiVersion: apps/v1
kind: Deployment # We push a deployment object
metadata:
  name: myapp # Deployment’s name
spec:
  selector:
    matchLabels: # The label of the pods to manage
      app: myapp
  replicas: 2 # Tells deployment to run 2 pods
  template: # Below is the classic definition of a pod
    metadata:
      labels:
        app: myapp # Label of the pod
    spec:
containers:
  - name: nginx  # First container
    image: sparcflow/nginx
    ports:
      - containerPort: 8080
  - name: mydb  # Second container
    image: redis
    ports:
      - containerPort: 6379
```

Listing 7-2: Re-creating our pod as a deployment object

Now we submit the manifest file and check the details of the new deployment pods:

```
root@DemLab:~# kubectl apply -f deployment_myapp.yaml
deployment.apps/myapp created
root@DemLab:~# kubectl get pods
```

| NAME | READY | STATUS | RESTARTS | AGE |
|------|-------|--------|----------|-----|
| myapp-7db4f7-btm6s | 2/2 | Running | 0 | 1m38s |
| myapp-9dc4ea-ltd3s | 2/2 | Running | 0 | 1m43s |

Figure 7-4 shows these two pods running.

![](img/961e81aef23040d0fbe348f58c055860_133_0.png)

Figure 7-4: Two pods running, each composed of two containers

All pods and nodes that are part of the same Kubernetes cluster can freely communicate with each other without having to use masquerading techniques such as Network Address Translation (NAT). This free communication is one of the defining network features of Kubernetes. Our pod A on machine B should be able to reach pod C on machine D by following normal routes defined at the machine/router/subnet/VPC level. These routes are automatically created by tools setting up the Kube cluster.

## Balancing Traffic

Now we want to balance traffic to these two pods. If one of them goes down, the packets should be automatically routed to the remaining pod while a new one is respawned. The object that describes this configuration is called a service and is depicted in Figure 7-5.

![](img/961e81aef23040d0fbe348f58c055860_134_0.png)

Figure 7-5: A cluster service object

A service’s manifest file is composed of metadata adding tags to this service and its routing rules, which state which pods to target and port to listen on (see Listing 7-3).

```
# myservice.yaml file
# Minimal description to start a service
apiVersion: v1
kind: Service # We are creating a service
metadata:
    name: myapp
    labels:
        app: myapp  # The service's tag
spec:
    selector:
        app: myapp # Target pods with the selector "app:myapp"
    ports:
    - protocol: TCP
      port: 80 # Service listens on port 80
      targetPort: 8080 # Forward traffic from port 80 to port 8080 on the pod
```

Listing 7-3: The service manifest file

We then submit this manifest file to create the service, and our service gets assigned a cluster IP that is reachable only from within the cluster:

```
root@DemLab:/# kubectl apply -f service_myapp.yaml
service/myapp created

root@DemLab:/# kubectl get svc myapp
```

| NAME | TYPE | CLUSTER-IP | EXTERNAL-IP | PORT(S) |
|------|------|------------|-------------|---------|
| myapp | ClusterIP | 10.100.166.225 | <none> | 80/TCP |

A pod on another machine that wants to communicate with our Nginx server will send its request to that cluster IP on port 80, which will then forward the traffic to port 8080 on one of the two containers.

Let’s quickly spring up a temporary container using the Docker public image curlimages/curl to test this setup and ping the cluster IP:

```
root@DemLab:/# kubectl run -it --rm --image curlimages/curl mycurl -- sh

/$ curl 10.100.166.225
<h1>Listening on port 8080</h1>
```
