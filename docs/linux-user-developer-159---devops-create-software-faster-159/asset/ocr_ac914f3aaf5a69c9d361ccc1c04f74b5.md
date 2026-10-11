# OpenSource

Your source of Linux news & views

# INTERVIEW MITCHELL HASHIMOTO

# Otto: Meet the new Vagrant

![](bbox=[0.06, 0.29, 0.27, 0.46])

Mitchell Hashimoto integrates development and deployment in Otto, the next generation of Vagrant. We asked how it will simplify software production for you

**What is Otto, in a nutshell?**

Its goal is to do everything as well as, if not better than, Vagrant could do from a developer perspective. And then we also added deployment. That’s the feature difference, but there are also philosophical differences.

The major philosophical difference is what we call fossilisation versus codification. If you take a Vagrantfile from five years ago and run **vagrant up** today, it’ll probably still work and bring up that environment exactly how you set it up five years ago. That’s because a Vagrantfile is a fossil – a snapshot in time. For some use cases you want a fossil, but what we’ve determined over the past few years is that what you really want is codification. So if you look at the AppFile, which is Otto’s configuration format, instead of being prescriptive on how to do something, it’s declarative on what you want to get done. So you’re saying, ‘1 want to develop a PHP application’, but you’re not saying how to install PHP, you’re not saying what OS to use, and that’s because the knowledge of how to do that is centralised in Otto. So if

you run Otto today and you run Otto five years from now, it’s likely that different things will happen because we’re going to use current best practices.

The main difference is that AppFile describes the application and Vagrantfile describes the machine.

**The website says that Otto is built for microservices – what do you mean by this?**

We went through a phase where there were a lot of monoliths and now we’re coming back to service- oriented, but with lots of little services versus a handful of bigger services. This has made development difficult because you need to know how to install a handful of services as well as your application, which might be in different languages – completely ignoring deployment. And so we tried to solve that with Otto, with the AppFile that you use to describe and configure Otto.

You put in the pointers to URLs where the dependencies are, and Otto reaches out to those, downloads them and reads their AppFiles, which describe how to install them for development. It puts

**Mitchell Hashimoto**, founder of HashiCorp, is a developer obsessed with automation. He is the creator of Vagrant, Packer, Serf, Consul, Terraform, Vault, Nomad and Otto. He is a key DevOps community figure, a technical author, and a seasoned engineer with enable experience in the fields of operations and research

# Otto and Atlas

Atlas is HashiCorp’s only commercial product, funding its eight open source projects. Mitchell tells us that Otto+Atlas (is like Git+GitHub – it gives you core workflow, all the primitives, a lot of the complextagic. Eventually, it will give you a full UI to Otto. Atlas will also be the collaboration platform for Otto, checking that nobody else is deploying a particular application at the same time as you, and enabling you to control which applications people can deploy, and even the times at which they can deploy them. Atlas will also be able to run a lot of the Otto commands for you, enabling you to offload activities and, for example, close your laptop while an **otto deploy** is running.

![](bbox=[0.28, 0.63, 0.91, 0.9])

**Above** Otto uses a declarative approach, which makes life much easier for developers

12