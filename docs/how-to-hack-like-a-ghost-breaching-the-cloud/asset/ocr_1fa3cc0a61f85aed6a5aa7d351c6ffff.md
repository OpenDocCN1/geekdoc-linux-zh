And finally, we also make sure to grab that GitHub token belonging to github-bot-ro. We make sure it is still valid by performing a quick API call using these few lines of Python code:

```
root@Point1:~/# python3 -m pip install PyGithub
root@Point1:~/# python3

>>> from github import Github
>>> g = Github("9c13d31aaedc0cc351dd12cc45ffafbe89848020")
>>> print(g.get_user().name)
mxrads-bot-ro
```

They were right after all. Kubernetes sure is fun!
We can safely say that we currently own MXR Ads’ delivery infrastructure. We still don’t know how the profile targeting works or who the end clients of Gretsch Politico are, but we can alter, delete, and block all their campaigns—and probably much more.
Before we dive even deeper into this rabbit hole, we need to secure the position we worked so hard to attain. Containers have a high volatility that puts our current access at risk. All it would take is a new deployment of the surveys app to kill our shell access—and with it, our main entry point to MXR Ads’ Kubernetes cluster.

# Resources

+   - More info about RBAC in Kubernetes: https://www.liquidweb.com/kb/kubernetes-rbac-authorization/.
- John Lambert’s seminal piece on the defender’s mindset: https://github.com/JohnLaTwC/Shared.
- An intro to JSON Web Tokens: http://bit.ly/35fTJyp.
- The Kubernetes API reference: https://www.sparcflow.com/docs/kube-api-v1.19.html.
- A list of Kubectl commands: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands.
- Information on OpenID, an authentication standard used to delegate authentication to a third party: https://developers.onelogin.com/openid-connect/.
- IAM roles attached to pods: https://docs.aws.amazon.com/eks/latest/userguide/worker_node_IAM_role.html.
- AWS docs on managing Auto Scaling groups for EKS: https://amzn.to/2uJeXQb.
- An exploration of network policies in Kubernetes: https://banzaicloud.com/blog/network-policy/.
- A walkthrough of installing Helm and Tiller on a Minikube cluster: http://bit.ly/2tgPBIQ
- An explanation of real-time bidding: https://digiday.com/media/what-is-real-time-bidding/.