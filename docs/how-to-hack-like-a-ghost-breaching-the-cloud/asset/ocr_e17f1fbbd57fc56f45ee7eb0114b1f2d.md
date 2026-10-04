far in the mountains, and push them over the edge. Kubernetes is no magic. It’s complex. It’s a messy spaghetti of dissonant ingredients somehow entangled together and bound by everyone’s worst nemeses: iptables and DNS.

The best part for us hackers? It took a team of very talented engineers two full years after the first public release to roll out security features. One could argue over their sense of priority, but I, for one, am grateful. If qualified, overpaid engineers were designing unauthenticated APIs and insecure systems in 2017, who am I to argue? Any help is much appreciated, folks.

Having said that, I believe that Kubernetes is a powerful and disruptive technology. It’s probably here to stay and has the potential to play such a critical role in a company’s architecture that I feel compelled to present a crash course on its internal workings. If you’ve already deployed clusters from scratch or written your own controller, you can skip this chapter. Otherwise, stick around. You may not become a Kube expert, but you will know enough to hack one, that I can promise you.

Hackers cannot be satisfied with the “magic” argument. We will break Kube apart, explore its components, and learn to spot some common misconfigurations. MXR Ads will be the perfect terrain for that. Get pumped to hack some Kube!

# Kubernetes Overview

Kubernetes is the answer to the question, “How can I efficiently manage a thousand containers?” If you play a little bit with the containers in the infrastructure we set up in Chapter 3, you will quickly hit some frustrating limits. For instance, to deploy a new version of a container image, you have to alter the user data and restart or roll out a new machine. Think about that: to reset a handful of processes, an operation that should take mere seconds, you have to provision a whole new machine. Similarly, the only way to scale out the environment dynamically—say, if you wanted to double the number of containers—is to multiply machines and hide them behind a load balancer. Our application comes in containers, but we can only act at the machine level.

Kube solves this and many more issues by providing an environment to run, manage, and schedule containers efficiently across multiple machines. Want to add two more Nginx containers? No problem. That’s literally one command away:

```
root@DemoLab:/# kubectl scale --replicas=3 deployment/nginx
```

Want to update the version of the Nginx container deployed in production? Now there’s no need to redeploy machines. Just ask Kube to roll out the new update, with no downtime:

```
root@DemoLab:/# kubectl set image deployment/nginx-deployment\
nginx=nginx:1.9.1 --record
```