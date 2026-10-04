forwarded to the KUBE-NODEPORTS chain. If the destination port matches a predeclar ed node port, the packet is forwarded to the load-balancing chain (KUBE-SVC-NPJI) we saw that distributes it randomly among the pods:

```
--snip--
-A KUBE-SERVICES -m comment --comment "last rule in this chain" -m addrtype --dst-type LOCAL -j KUBE-NODEPORTS

-A KUBE-NODEPORTS -p tcp -m tcp --dport 31357 -j KUBE-SVC-NPJI
```

That's all there is to it: a clever chain of iptables rules and network routes.

In Kubernetes, every little task is performed by a dedicated component. Kube-proxy is in charge of the networking configuration. It is special in that it runs as a pod on every node, while the rest of the core components run inside multiple pods on a select group of nodes called master nodes.

Out of the 100 nodes we made when we created the cluster of 100 machines, the one master node will host a collection of pods that make up the spinal cord of Kubernetes: the API server, kube-scheduler, and controller manager (see Figure 7-6).

![](bbox=[0.23, 0.46, 0.87, 0.68])

Figure 7-6: Pods running on the master node versus those running on regular nodes

NOTE In a multimaster setup, we will have three or more replicas of each of these pods, but only one active pod per service at any given time.

We actually already interacted with the master node when using kubectl apply commands to send manifest files. Kubectl is a wrapper that sends HTTP requests to the all-important API server pod, the main entry point to retrieve and persist the famous desired state of the cluster. Here is a typical configuration one may use to reach the Kube cluster (~/kube/config):

```
apiVersion: v1
kind: Config
clusters:
- cluster:
```