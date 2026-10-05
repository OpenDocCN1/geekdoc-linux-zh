
# OffSec

The Learning Modules also contain various exercises. Completing the Module exercises will help you become more efficient with discovering and exploiting the vulnerabilities in the lab machines.

Some Module exercises have a simple question-and-answer where the learner is tasked with retrieving the solution from the text. Other Module exercises have three components: a question, a machine (or a group of machines), and a flag. In these cases, the question asks you to perform a specific action or set of actions on the provided machine. Once you have successfully completed the objective, you will receive a flag in the OS(random-hash). You can then submit the flag into the OffSec Learning Portal (OLP), which will tell you if you have inserted the correct flag or not. The OLP will then view your progress, and track the number of your correct submissions provided to date.

It is worth noting that flags are dynamically generated at machine boot and expire at machine shutdown. If the solution is obtained to a question and the machine is reverted, and only after the revert answer is submitted, the OLP will not accept the flag.

> The flag must be submitted before reverting or powering off the machine.

As an additional note, the way Module exercises are implemented allows us to use the same IP and port multiple times. On the Module Exercise VMs that require an SSH connection, we suggest using the SSH command with a couple of options as follows:

```bash
ssh -o "UserKnownHostsFile=/dev/null" -o "StrictHostKeyChecking=no"
learner@192.168.50.52
```

Listing 1 - The "recommended" way to SSH into Module Exercise VMs

The UserKnownHostsFile=/dev/null and StrictHostKeyChecking=no options have been added to prevent the known-hosts file on your local Kali machine from being corrupted.

> Module Exercises are currently supported on the x86-64 Kali Linux version exclusively

We will get over the design of different kinds of Module exercises in a section below.

## 2.1.2 Student Mentors and Support

Discord, our community chat platform, can be accessed via the Profile drop-down at the upper right corner of the OffSec Learning Portal. Live Support will allow you to directly communicate with our Student Mentors and Technical Support Teams.

The Technical Support Team is available to assist with technical issues, with the Student Mentors will be able to clarify items in the course material and exercises. In addition, if you have tried your best and are completely stuck on an exercise or lab machine, Student Mentors may be able to provide a small hint to help you on your way.

Remember the information provided by the Student Mentors will be based on the amount of detail you are able to provide. The more detail you can give about what you've already tried and the outcomes you've been able to observe, the more they will be able to help you.

## 2.1.3 Setting up Kali

The Module Exercises and Challenge Labs are to be completed using virtual machines (VMs) operating in our lab environment. When we refer to a lab environment, we mean the combination of the following components:

- Your Kali Linux VM
- The OffSec Learning Portal
- A lab containing deployable target machines
- A VPN connection between your Kali VM and the lab

Let's look at these components individually.

Kali Linux is an operating system (like Windows or macOS) that comes with a curated set of tools that are specifically used for penetration testing and other information security activities. Kali Linux is open source and free.

If you're already familiar with cybersecurity, you may have Kali Linux installed and can skip ahead to the next section.

If not, strongly recommend installing Kali on a VM, which provides the functionality of a physical computer running another operating system (OS) within a program called a hypervisor. The benefit of using a VM is that it allows us to run a guest OS over a host OS. Although you could install Kali on a dedicated machine, it is more convenient, safe, and efficient to install Kali within our host system. Among other reasons, this ensures that we have easy access to all the tools available to both.

For example, we may be using a desktop computer running Windows or a laptop running macOS. We could install VMware Workstation Player on our Windows machine or VMware Fusion on Mac to install the Kali Linux image. When this virtual image is installed, Kali will run alongside our primary operating system in a window, or full-screen if we configured properly. Kali Linux will have access to the network with its IP address and behave as if it's installed on a dedicated machine for the most part.

> From a terminology standpoint, we call the physical system running Windows or macOS our host machine and we call the Kali VM a guest machine.

The VMware image that we recommend is a default 64-bit build of Kali Linux. We recommend using the latest VMware image available on the OffSec VM download page. Note that although the VirtualBox image, the Hyper-V image, or a dedicated installation of Kali should work, we can only provide support for the indicated VMware images.

In the next section, we'll set up the VPN connection that will connect us to the lab.

## 2.1.4 Connecting to the PWK Lab

Many of the Module exercises and all of the lab machines will require you to connect to a Virtual Private Network (VPN).

A VPN essentially creates an encrypted tunnel that allows your data to traverse an open network such as the public Internet, and connect to another isolated network securely.

We'll connect to the VPN from our Kali machine, granting access to the lab. When a learner connects to the lab, the specific segment of the network they connect to is private to them. In other words, each connection is a unique environment where the learner can work at their own pace without worrying about interrupting, or interrupted by, other learners.

Even though kali is private, it is prudent to consider the labs as a hostile environment and should not store sensitive information on the Kali Linux virtual machine used to connect to the VPN. Client-to-client VPN traffic is strictly forbidden and could result in termination of access from the course and its materials.

Fortunately, connecting to a VPN is a quick and easy process. If you're using Kali as a VM, go ahead and start the machine. Then on the Kali machine, open a browser and navigate to the OffSec Learning Portal and sign in.

Next, let's navigate to the Course drop-down menu and select the PEN200 course. This will take us to the main course page. At the top right corner of the page to the left of your account name, you will see the drop-down menu for VPN. Clicking this option will generate a VPN pack for your course and download it in the form of a .ovpn file. Be sure to note the location of the download.

Next, let's use the Kali terminal to connect to the VPN. Clicking the black terminal icon at the top-left of the Kali VM will prompt a window like this:

```bash
learner@kali:~$
```
