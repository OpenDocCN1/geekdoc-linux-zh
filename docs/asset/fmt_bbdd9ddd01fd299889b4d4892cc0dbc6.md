
```
root@k8master:/etc# export KUBECONFIG=/etc/kubernetes/admin.conf

root@k8master:/etc# kubectl get nodes

NAME STATUS ROLES AGE VERSION

k8master Ready control-plane 3m41s v1.28.3

k8sworker1 Ready <none> 46s v1.28.3

root@k8master:/etc#
```
