One pod is great, but two are better, especially for resilience so the second can act as a backup should the first fail. What should we do? Submit the same manifest twice? Nah, we create a deployment object that can replicate pods, as depicted in Figure 7-3.

![](bbox=[0.24, 0.14, 0.66, 0.31])

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
```