much attention since being launched in 2013 – No more ‘Well, it worked on my machine’ type arguments between programmers and operations staff when a system goes live and fails to deploy properly in production!

# Little boxes, little boxes

With the promise of DevOps utopia ahead of us, let’s waste no further time and get on with the business of installing Docker. At the time of writing, Ubuntu 14.04 has version 0.91 of the software in it’s repositories. Let’s live a little more (or possibly less) dangerously to note: on Debian based systems, the maintained package is called docker.io, as the docker name was grabbed by a ‘system tray for kde/gnome docker applications’ some time ago. Red Hat based systems stick with ‘docker’.

Docker provides a handy little script for ensuring our system can work with https apt sources and adds its repo to our sources and its key to our keyring before installing the package. Run the following to take a look at it (it’s generally good practice to give a program at least a cursory check before running it on your system).

```
curl -sSL https://get.docker.io/ubuntu/
```

Once you’re happy that it’s not installing the latest NSA backdoor or foreign Bitcoin stealing malware you can let it do it’s thing:

```
curl -sSL https://get.docker.io/ubuntu/ | sudo sh
```

This will then install a handful of packages and start a docker daemon process, which you can confirm is running via the ps command. Instructions for other distributions can be found on the official site (http://bit.ly/DockerInstalls). Now let’s dive right in with the traditional ‘Hello, World!’ to give us confirmation that everything is working as intended!

```
sudo docker run ubuntu /bin/echo "Hello, World!"
```

You will see a message saying that an Ubuntu image can’t be found locally, and one will be downloaded (via the Docker Hub) as well as a number of updates. Thankfully, once an image is downloaded it remains cached and subsequent runs are much quicker. Once everything is ready, the magic words will appear. But what’s happening here? The docker run command does exactly what you’d expect: it runs a container. We asked for an Ubuntu image to be used for the container, which Docker pulled from its hub when it couldn’t find a local copy. Finally, we asked for the simple echo command to be run inside it. Once Docker completed its tasks, the container was shut down. We can use this downloaded image in a more interactive way by using the -i and -t flags, which enable us to use the containers STDIN and give us a terminal connection.

```
sudo docker run -i -t ubuntu /bin/bash
```

This should give a root prompt almost immediately within the container itself. The speed with which that hopefully appeared is one of the reasons for Dockers popularity. Containers are very fast and lightweight. Many of them can co-exist on a system, many more than could be handled if they were more like traditional heavy virtual machines. This is partly due to Docker using union file systems which are file systems that operate by creating layers. This makes them extremely fast. As you would expect, Linux comes with more than one variant. Docker by default uses devicemapper, but also supports AUFS, btrfs and vfs.

From that prompt, run a few commands such as df -h, ls and finally top. While the first two should look pretty vanilla as far as output goes, top will show a rather odd situation of only two running processes: bash and the top command itself. Exit this strange matrix like situation by pressing q (to come

![](bbox=[0.47, 0.62, 0.88, 0.82])

The Docker website – no pale whale here – and includes a live online tutorial which runs through the basics in roughly 10 minutes.

# Hypervisors vs Containers – what’s the difference?

These days, there are a huge range of options available for a sysadmin to consider when asked to architect new infrastructure. Anyone can be forgiven for getting lost in the virtualisation maze. So what exactly is the difference between a hypervisor- and a container-based system? Hypervisors, which have their origins in the IBM systems of the 1960s, work by having a host system share hardware resources amongst guest systems (or virtual machines). The hypervisor manages the execution of guest operating systems and presents virtualised representations of the underlying resources to them. There are a couple of different types:

Type 1 hypervisors These are installed before any guest systems and work directly with the underlying hardware (VMware is an example of this approach).

Type 2 hypervisors Run on top of a traditional operating system, with the guests at another level above that (this is how Virtualbox works).

Containers however, work by having the kernel of an operating system run isolated processes in ‘userspace’ (ie outside of the kernel). This can be just a single application and, therefore, doesn’t need the overhead of a full OS (which then needs maintenance, patching etc). Containers also have the bonus of being very lightweight. In fact, many containers can run on the same hardware but can’t run ‘other’ operating systems (eg Windows) and are, as a consequence, seen as not being as inherently secure as hypervisors.

As usual, it’s a case of using what virtualisation technology is best for a particular situation or environment. Issues of cost, existing systems, management tools and skill sets should be considered. However the two approaches are not mutually exclusive and indeed can be complementary – quite a few adopters of Docker have confessed to running it within hypervisor based guests. Virtualisation is an active area of development, with open source at the forefront.

Quick tip LXC (Linux Containers) can refer to both the underlying capabilities of the kernel (cgroups et al) and also to the project that maintains the userland tools – which is well worth a look and has reached version 1.0.

More networking Keep track of everything with Zabbix, see p118.