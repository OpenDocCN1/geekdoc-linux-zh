
## Introduction 756
## Overview 756
## Preparing for a Custom JumpStart Installation 758
## What Happens During a Custom JumpStart Installation? 759
### Boot Server 760
### The Install Server 764
### Configuration Server 766
## The Rules File 769
### Validating the Rules File 776
### Begin and finish Scripts 778
## Creating Class Files 779
### backup_media 780
### boot_device 781
### client_arch 782
### client_root 783
### client_swap 783
### cluster 784
### dontuse 785
### filesys 785
### install_type 788
### geo 789
### isa_bits 790
### layout_constraint 790
### locale 792
### num_clients 792
### package 793
### partitioning 793
### root_device 794
### system_type 794
### usedisk 795
## Testing Class files 795
## sysidcfg file 798
## Name Service, Domain Name, and Name Server Keywords 799
### Network-Related Keywords 800
### Setting the Root Password 801
### Setting the System Locale, Terminal, Timezone, and Time Server 802
## Setting Up JumpStart in a Name Service Environment 803
## Setting Up Clients 803
## A Sample JumpStart Installation 806
### Setting Up the Install Server 806
### Creating the JumpStart Directory 807
### Setting Up a Configuration Server 808
### Setting Up Clients 809
### Starting Up the Clients 809
## Summary 812
## Apply Your Knowledge 813

## STUDY STRATEGIES

The following strategies will help you prepare for the test:

- Practice the step-by-step examples that I provide in this chapter on a Solaris system. Be sure that you understand every step and can describe the process of setting up a boot server, an install server, and a configuration server. You should also be able to identify the events that occur during the JumpStart client boot sequence.
- Understand each of the commands I've described. Get familiar with all the options, especially those that I used in the examples. You'll see questions related to the add_install_client, add_to_install_server, and modify_install_server scripts.
- State the purpose of the sysidcfg file, the class file, and the rules file. Given the appropriate software source, be prepared to explain how to create a configuration server with a customized rules file and class files.
- State the purpose of the JumpStart server, and identify the main components of each type of server. Learn the terms I've listed in the “Key Terms” section of this chapter. Be prepared to provide a description of each term.

## INTRODUCTION

There are four ways to install the Solaris software on a system: interactive installation (described in Chapter 3, “Installing the Solaris 8 Software”), custom JumpStart (described in this chapter), Web Start (described in Appendix A, “Web Start”), and installation over the network (also described in Chapter 3). To install the operating system (OS) on a server, you’ll use the interactive method described in Chapter 15, “Installing a Server.” This chapter describes how to install the Solaris OS on clients using the custom JumpStart method.

## OVERVIEW

There are two versions of JumpStart: JumpStart and custom JumpStart. JumpStart lets you automatically install the Solaris software on a SPARC-based system just by inserting the Solaris CD and powering on the system. You do not need to specify the boot command at the ok prompt. The software that is installed is specified by a default class file that is chosen based on the system’s model and the size of its disks; you can’t choose the software that is installed. For new SPARC systems shipped from Sun, this is the default method of installing the OS when you first power on the system.

The custom JumpStart method of installing the OS provides a way to install groups of similar systems automatically and identically. If you use the interactive method to install the OS, you must carry on a dialogue with the installation program by answering various questions. At a large site with several systems that are to be configured exactly the same, this task can be monotonous and time-consuming. In addition, there is no guarantee that each system will be set up the same. Custom JumpStart solves this problem by providing a method to create sets of configuration files beforehand so that the installation process can use them to configure each system.

Custom JumpStart requires up-front work, creating custom configuration files before the systems can be installed, but it’s the most efficient way to centralize and automate the OS installation at large enterprise sites. Custom JumpStart can be set up to be completely “hands off.”

NOTE
You’ll see the class file referred to as the profile in many Sun documents, scripts, and programs that relate to JumpStart. In the Sun System Administration training classes, however, it is referred to as class file. That’s how I’ll refer to it throughout this chapter. On the exams, it will also be referred to as a class file. The same is true for the configuration server. Sometimes Sun will refer to this server as a profile server.

The custom configuration files that need to be created for JumpStart are the rules and class files. Both of these files consist of several keywords and values, and are described in this chapter.

Table 21.1 lists the various commands that are introduced in this chapter.

## TABLE 21.1
JumpStart Commands

| Command | Description |
|---|---|
| setup_install_server | Sets up an install server to provide the OS to the client during a JumpStart installation. |
| add_to_install_server | A script that copies additional packages within a product tree on the Solaris 8 Software and Solaris 8 Languages CDs to the local disk on an existing install server. |
| modify_install_server | A script that adds the Solaris Web Start user interface software to the Solaris 8 Software and Solaris 8 Languages CD images on an existing install server, thus enabling users to use Solaris Web Start to boot a system and install the Solaris 8 software over a network. |
| add_install_client | A command that adds network installation information about a system to an install or boot server's /etc files so the system can install over the network. |
| rm_install_client | Removes JumpStart clients that were previously set up for network installation. |
| check | Validates the information in the rules file. |
| pfinstall | Performs a “dry run” installation to test the class file. |
| patchadd -C | A command to add patches to the files located in the miniroot (that is, Solaris_8/Tools/Boot) on an image of an installation CD image created by setup_install_server. This facility enables you to patch Solaris installation commands and other miniroot-specific commands. |

NOTE
At times, I describe the boot server, the install server, and the configuration server as if they are three separate systems. The reality, however, is that most companies have one system that performs all three functions. I'll describe this in more detail in the “Install Server” section later in this chapter.

There are three main components to JumpStart:

- Boot and Client Identification Services. These services are provided by a networked boot server, and provide the information that a JumpStart client needs to boot using the network.
- Installation Services. These are provided by a networked install server, which provides an image of the Solaris Operating Environment the JumpStart client uses as its source of data to install.
- Configuration Services. These are provided by a networked configuration server, and provides information that a JumpStart client uses to partition disks and create file systems, add or remove Solaris packages, and perform other configuration tasks.

Each of these components is described in this chapter. If any of these three components is improperly configured, the JumpStart clients can:

- Fail to boot.
- Fail to find a Solaris Operating Environment to load.
- Ask questions interactively for configuration.
- Fail to partition disks, create file systems, and load the operating environment.

## PREPARING FOR A CUSTOM JUMPSTART INSTALLATION

The first step in preparing a custom JumpStart installation is to decide how you want the systems at your site to be installed. Here are some questions that need to be answered before you begin:

- Will the installation be an initial installation or an upgrade?
- What applications will the system support?
- Who will use the system?
- How much swap space is required?
