### Mostafa Abd-ElHamid Atwa

# Linux for system administrators and DevOps

Linux for system administrators and DevOps

1st edition

© 2015 Mostafa Abd-ElHamid Atwa & [bookboon.com](http://bookboon.com)

ISBN 978-87-403-1137-2

# Disclaimer

The information in this document is based on publicly available documentation’s and author’s personal & professional experience. In no event shall author be liable for any direct, indirect, consequential, punitive, special or incidental damages (including, without limitation, damages for loss of profits, business interruption or loss of information) arising out of the use or inability to use this document, even if Author has been advised of the possibility of such damages. Author makes no representations or warranties with respect to the accuracy or completeness of the contents of this document and reserves the right to make changes to this document at any time without notice. Author does not make any commitment to update the information contained in this document.

For Manon Niazi, the Deutchlander, I still like the college days as it was happening yesterday.

For my mother and family.

For the soul of my heavenly father.

Thanks for everyone.

# Introduction

This book is dedicated for LINUX engineers, system administrators and devops who can use the materials illustrated in this book in most of their daily tasks during work.

It can transform you from basic-novice LINUX related engineer or an engineer with no-experience in LINUX environments to an experienced and advanced LINUX professional.

![](image/Image960.jpg)

# 1 Linux Desktop, Server and Cloud  Image

## 1.1 What is Linux?

LINUX is a community open source operating system developed by LINUS TORVALDS under the model of free and open source software development and distribution.

LINUX was originally developed for Intel® x86 Architecture.

The LINUX operating system was intended for mainframe computers and large-scale server systems, but now it is running on desktop machines, tablets, and smart phones.

LINUX Distributions are based on 6 distributions:

1.  Debian Based
2.  Gentoo Based
3.  Pacman Based
4.  RPM-Based
5.  Slackware Based
6.  Independent

Most of the book material is dependent on LINUX DEBIAN UBUNTU and as the time of writing this book on version 15.04.

Honestly I have choose this distribution because it is the most supportive and popular distribution and flavor of all the LINUX operating system distributions and ranked number 1 across the LINUX family.

## 1.2 Linux GUI and Desktop Machines

If you are comparing LINUX to other operating systems, yes, it has a Graphical User Interface or GUI, so it can be easy for non-professional computer scientists and engineers to use, yes it is usable by regular non-computer-professional end-users.

You can switch between desktops, browse folders, share files and do most of the basic regular usage on it every day.

You can manipulate folders, files, create images, browse the Internet, etc.

You can also create a network of computers, share printers and files, you can create print servers, make word processing, and you can operate the machine easily as you want to do any task during your working day, and even at home, or on your phone, it can now manage your phone calls, and you can use it on your tablet to create and send e-mails, browse the Internet and more…

![](image/Image967.jpg)

## 1.3 Linux Servers and Clusters

LINUX servers are machines intended for servicing other types of computers and devices like desktops, tablets, and mobile phones.

It can also manage your storage devices, network devices, and any machine that is capable of being connected to the computer infrastructure.

The focus of the study of this book is to do server-client infrastructure and management of LINUX environment containing desktop, tablet, mobile and server machines.

![](image/Image976.jpg)

Server Distribution Versions of LINUX are equipped with a terminal screen as the user interface screen and mostly does not contain any graphical user interface for the sake of security and performance.

We will talk about what is the terminal screen in chapter VI customizing LINUX shell and you will gain more information about the shell environment and basic shell commands.

You can take a look around you to get to notice what are the capabilities of servers and what can the server do for you and your environment.

For example if you look at the mail services like your company mail service, your free service provider that provide mail services for free over the Internet or for profit.

The mail server is used to save all the mail messages that you send, receive and you partially write and save on a large storage media precisely allocated for mail messages, attachments, drafts etcetera and specialized for the privacy of every user using user account authentication and authorization with security mechanisms.

Another example of the server-client environment is when you use your drive account on any cloud storage provider or you use a mapped network drive on your company’s environment, this is simply a storage server with an FTP, SFTP protocols installed on a server machines and mapped to network drives on your working machine.

A sample server-client environment infrastructure can be illustrated in figure 1.1.

![](image/Image984.jpg)

**Figure 1.1** Shows a Sample Network Infrastructure Environment

This infrastructure contains regular PC computers, laptops, tablets, mobiles, printers, scanners, ISP wireless device, modem, storage router software, storage tapes, cluster, workstation, etcetera.

The client here in this infrastructure is represented by the PC, laptop, scanner, printer, and tablet devices and server is represented by the cluster, storage router, tapes, and workstation.

There are also network mediums that transfer data between devices like the wireless device in the middle and the modem device at the bottom of the cluster.

## 1.4 Linux Cloud Images and Virtual Machines

LINUX cloud images are minimized versions of LINUX distributions working with minimal configuration options and features optimized for cloud environments.

The minimization of LINUX cloud images is for performance and disk occupation, which will also allow the user to get rid of the idle features that do not fit the environment the user is intending the build like for example if the user is building a web server environment, the user will have only to install the features of the web server environment without the need to have all other LINUX features.

LINUX cloud images have a terminal user interface and does not include any graphical user interface in it.

LINUX cloud images are built on the same distribution flavors that we mentioned earlier in the section named #What is LINUX?|outline

Cloud images are used to be deployed into virtual machines and you can also deploy complete LINUX images on virtual machines.

You can use Cloud Images to deploy it on cloud operating systems like OpenStack® and AWS (Amazon Web Services) EC2 (Elastic Compute Cloud) or other cloud provider companies.

Cloud images can be in 32bit and 64bit architectures based on the processor of the hardware you are using, you can install the suitable cloud image on the suitable virtual machine you have assigned on that hardware processor.

Cloud images for example can be downloaded from the following URLs:

[https://cloud-images.ubuntu.com/](https://cloud-images.ubuntu.com/)

[https://aws.amazon.com/marketplace/ref=mkt_ste_amis_redirect?b_k=291](https://aws.amazon.com/marketplace/ref=mkt_ste_amis_redirect?b_k=291)

These links are not permanent and if you found a change within these links, you can search for cloud images over the Internet to download any of these images.

We will talk about virtual machines later in a topic called LINUX virtual machines.

## 1.5 Linux Distributions and Flavors

As mentioned earlier in a previous topic called #What is LINUX?|outline we can tell that LINUX flavors do not have different architectures or performance variations, but they vary in the distribution’s commands to perform various installations for example:

UBUNTU®: We use the following command to update the operating system

sudo apt-get update

FEDORA®: We use the following command to update the operating system

sudo yum install update

And in other distributions it may vary a little bit than these commands but all of these commands are performing system update.

It may also vary in the package name (program name) you are installing on different distributions like for example:

Installing MySQL database server on fedora may differ than installing it on UBUNTU® as follows:

UBUNTU®: We use the following command to install MySQL server

sudo apt-get install mysql-server

FEDORA®: We use the following command to install MySQL server

sudo yum install mysql-community-server

So the package name has changed from UBUNTU® repositories to FEDORA® repositories from mysql-server in UBUNTU® to mysql-community-server in FEDORA®

And finally you need to be adopting your command to the distribution you are working on.

If you are installing a package (program), you need to know what is the exact package name of the distribution you are working on or performing this command on or if you are performing operating system optimization command, you also need to know each command on each distribution and execute the command which is suitable for the distribution.

## 1.6 Customizing Linux Shell

Some users need to customize the LINUX shell when performing tasks.

The LINUX terminal or shell window looks like figure 1.2

![](image/Image991.jpg)

We can perform command on this terminal window, and as you can see it, it is much similar like a minimal text editor for entering the installing and system manipulation commands.

This window can be customized according to the user needs like changing the background color and text color.

This window also can run commands as administrator power by using “sudo” keyword or by switching to the super user for the session you are currently working on by using the command sudo -s which will transfer you to the sudo privilege of the root user and you will notice that you will be using
[root@youroscomputername](mailto:root@youroscomputername).

![](image/Image999.jpg)

**Figure 1.3** shows you how this command is performed on an UBUNTU distribution.

This way, you can perform all the commands using power user (sudoer) or administrator or root user.

## 1.7 Basic Linux Commands

sudo apt-get update --fix-missing && sudo apt-get upgrade --fix-missing && sudo apt-get dist-upgrade –fix-missing

And you will see the output of this command in figure 1.4

![](image/Image1008.jpg)

**Figure 1.4** shows the update and upgrade process of UBUNTU LINUX distribution.

This command is used to completely update your LINUX distribution from using LINUX repositories that is belonging to the country where you are using the distribution.

**Notice that we use the “--fix-missing” key to switch to alternative packages in case of any failure, and you can also use this key with other commands if possible.**

If you want to use the main server repositories instead of country specific repositories, please run the following command:

sudo nano /etc/apt/sources.list

The output of the command will be as what figure 1.5 shows

![](image/Image1015.jpg)

You need to go up and down using arrow keys on your keyboard to reach to the line that you want to edit.

Locate all the country area in each line in my file here it is “eg.” in every line and remove it completely. Example “deb [http://eg.archive.ubuntu.com/ubuntu/](http://eg.archive.ubuntu.com/ubuntu/) vivid-updates main restricted” to “dev htp://archive.ubuntu.com/ubuntu/ vivid-updates main restricted” and you are good to go.

After performing these changes to the file, press CTRL+X on your keyboard to close the file. Notice that it is prompting you to save the file and choose the file name. You can just press Y on your keyboard and hit enter to save to the same file name and same directory.

Continuing basic commands for your LINUX environment, we can also get to know other commands which are very useful in every day system administration tasks.

To get all the running programs and processes on your LINUX distribution type the following command in the terminal window:

ps aux | less

The output of the command will be as what figure 1.6 shows:

![](image/Image1023.jpg)

You can go to the next line by pressing ENTER key on your keyboard for every line, then you can exit using the CTRL + Z to quit this command output screen and go back to the terminal original prompt.

One of the commands that also will be one of the most favorable is how to create a SWAP file used to strengthen the computer performance and LINUX will use it as RAM as follows:

sudo dd if=/dev/zero of=/swapfile bs=1G count=4

This command will make a SWAP file on the root directory of your LINUX distribution that will contain 4 portions [count=4] and will be divided into 4 partitions, every partition will be 1 Giga Byte [bs=1G].

The output of the command will be as figure 1.7 shows.

![](image/Image1031.jpg)

This way, you have created the SWAP file and the next step is to use it and make it available for your LINUX distribution (inform your LINUX distribution) to use it.

You need to adjust the privileges and ownership of the file that we have created by using the following command:

sudo chmod 600 /swapfile

This command does not have any output and it will return you to the prompt again without any text to appear after executing this command. In this command we have used “chmod” which is short for change mode of the file and we used 600 as an aliased number for assigning privileges to the file and make it only available to the operating system authorized users who can manipulate this kind of file, then we gave it the file path using /swapfile directive.

After all we use this command to make the swap file:

sudo mkswap /swapfile

The output of the command is shown in figure 1.8 confirming that the command has been successfully executed.

![](image/Image1038.jpg)

We finally turn on the SWAP file using this command:

sudo swapon /swapfile

And this command does not show any output or text confirming the command success.

But we can confirm that the file has been successfully allocated by using this command:

![](image/Image1048.jpg)

Now the command output confirming that the file has been created successfully and working as required.

Continuing our basic commands section, we still can perform some terminal tasks that can be very useful in everyday LINUX administrator tasks:

How to manage services on LINUX machine and how to kill a process that you do not need after listing all the processes and identifying which process you need to kill will be covered in the following section.

By running this command you will be able to identify all the processes running on a LINUX machine and will identify every process using the process id as follows:

sudo swapon -s

By running this command, you will get a list of the processes with the process id as PID and figure 1.9 shows the output of this commands

By identifying the process using the PID you can use the following command to terminate this process

sudo kill -9 PID

![](image/Image1055.jpg)

As shown in figure 1.10, you need to replace the PID with the ID of the process you want to top, in my case I have stopped mysqld using the PID 14846.

![](image/Image1062.jpg)

Finally you can use the following command to start, stop and restart any service that you want

sudo service apache2 start

sudo service apache2 stop

sudo service apache2 restart

This command does not give any output or text indicating success but in case of failure, you will be notified with a notice indicating failure with reason according to the specific service you are managing.

In my case I have apache2 installed on my distribution and I have started, stopped, and restarted it in these 3 commands.

The following section will be containing useful links on how to work with LINUX shell.

[https://help.ubuntu.com/community/UsingTheTerminal](https://help.ubuntu.com/community/UsingTheTerminal)

[http://www.fedorafaq.org/basics/](http://www.fedorafaq.org/basics/)

## 1.8 Basics in Shell Programming

Shell programming is a kind of programming language specified for LINUX machines to make specific tasks related to your LINUX operating system’s environment.

In this section we need to be familiar with programming and how to use the LINUX shell to make a shell script that is containing some tasks for the terminal to do.

Let us start by getting to know what is programming:

Programming is a set of instructions and control and structure statements written in order for the machine to understand and perform. It must be in a standard syntax format so the machine can understand it. It must be sequenced one after another and you much check which one of the statement to be performed first, second, third etcetera to make the computer achieve the task you need it to do.

First we need to identify what is a shell script file and how can we create one of these files, then list our commands that does a specific task into this file, then run this file in a terminal window as follows:

1.  touch helloworld.sh
2.  nano helloworld.sh
3.  echo “Hello World”
4.  Press CTRL + X and then type y then hit enter key on your keyboard.
5.  sh helloworld.sh

    This will give the output Hello World in your screen on the terminal window.

What we did now is a kind of shell script file containing one single command that tells the computer to output the sentence Hello World.

*   First we created a file called helloworld.sh using the command touch helloworld.sh
*   Second we edited the file using a program called nano using this command nano helloworld.sh
*   Third we added one line into this file telling the computer to output a Hello World sentence to the screen using the echo command in terminal by the use of this command echo “Hello World”.
*   Fourth we saved the file using CTRL + X on your keyboard and confirming by typing Y, then pressing enter to use the same file name and directory.
*   Finally, we executed this script using sh command and pointing to the file name that we created in the previous steps using this command sh helloworld.sh and gave us the output as the following figure 1.11 shows us:

![](image/Image1070.jpg)

This way you have created a file into a shell script, entered a command in it and executed this command.

You can perform the previous steps with a list of commands under each other into this file after executing the nano command and starting editing the shell script file.

Let us make a loop that iterate with a condition:

Loops are used to make the computer do a task or a punch of tasks when a condition is met and stops when the condition is not met as follows:

1.  touch iterationofdays.sh
2.  nano iterationofdays.sh
3.  i=1
4.  weekdays=”Mon Tue Wed Thu Fri”
5.  for day in $weekdays
6.  do
7.  echo “Weekday $day”
8.  done
9.  Press CTRL + X on your keyboard, follow it by Y, then press enter to exit.
10.  sh iterationofdays.sh

In this example we did a series of commands that will be illustrated in the following points:

First: We created our shell script file using the touch command as we did in the previous example.

Second: We edited the file using nano editor.

Third: We inserted the variable called i and gave it the default value of 1.

Fourth: We created a list called weekdays and added values of week days separated by spaces, and enclosed with double quotation marks.

Fifth: We started a for statement to process the iteration that will be conditioned with 1 condition to loop until the end of the list that we have created in the fourth step.

Sixth: We started instructing the computer to do something as long as the for statement in step five is looping using the do command.

Seventh: We gave some orders to the computer to output the day name in the command we gave it to the screen.

Eighth: We ended the commands we gave the computer to do by using done keyword.

Ninth: We have closed and saved the shell script file that we created in the first step.

Tenth: We executed the file using the command sh iterationofdays.sh

![](image/Image1078.jpg)

**Figure 1.12** shows the output of the script that we have created and procedures we did above.

Now that we need to know a little more about what we added in the file we created:

The variable is a place in memory that we can save data on and the name variable because we can change the data stored in it to any value that we want.

We use $ dollar sign to call the variable that we have created and use it in any statement in the script.

## 1.9 Installation Commands and Packages Configurations

Installation commands may vary according to the target program or package that you want to install.

The following commands examples can be used to install different packages and programs:

sudo apt-get install apache2

This command will make you install apache2 web server on your machine.

sudo java -jar filename.jar

This command will make you install a java jar type file.

sudo sh netbeans.sh

This command will make you install a shell type file on the terminal.

These commands can also vary according to the file place you will install and examples are as follows:

sudo sh /home/username/Downloads/netbeans.sh

In case you have downloaded the file from the Internet on your machine and the file is now located for example insudo apt-get install oracle-java8-installer the default downloads directory:

You need to provide the full path of the file as follows: /home/username/Downloads/filename.sh

Some shortcuts can be put into practice while using the LINUX terminal as follows:

If you want to directly access the Downloads default directory in you LINUX machine, you can simply type: ~/Downloads/filename.sh

This way you eliminated the use of /home/username/ by using ~/ only.

Another shortcut example is by using ~/Desktop/filename.sh you are accessing a file located on your desktop directory.

If you want to browse the content of a directory to get the files within this directory use the following command:

ls -l /path/to/directory/

An example that shows how this command works with its output will be in the next figure 1.13.

![](image/Image1085.jpg)

One more thing to go, is when you perform a java -jar file installation or execution, you need first to have java sdk installed on your machine and this can be done using the following command:

sudo apt-get install openjdk-8-jre

And if you want the Oracle version of java, you can use the following commands to install it:

sudo add-apt-repository ppa:webupd8team/java -y

sudo apt-get update

sudo apt-get install oracle-java8-installer

Be very careful when installing these commands and examine exactly what to install before performing the installation steps.

## 1.10 Working with Repositories

Working with repositories on UBUNTU terminal is easy and configurable.

You can add a repository, manage repositories and use these repositories in your installations and system update.

Repositories are assemblies of installation and update files grouped together in one place with a unique URL that can be bound to your system using a file called sources.list and this file can be edited using a regular text editor and can be modified also using the terminal.

1st Lets add a repository to our sources.list file by using this command:

sudo add-apt-repository ppa:webupd8team/java -y

The output of this command is shown in figure 1.14

![](image/Image1093.jpg)

This command has added a java installation repository to the sources.list file, so that the operating system can recognize the package name for the java sdk program that we want to install.

We can edit the sources.list file by using the following command:

nano /etc/apt/sources.list

The command will be presenting a list of repositories where the operating system finds package names and recognize where to download and update these  packages.

You can edit in the file, add, update or delete any record you need but be very cautious when working with this file because it contains some sensitive data about updating and upgrading packages of your operating system.

## 1.11 Updates, Upgrades and Distributions Upgrades

Updating your machine is not a hard task unless you do not have much programs and packages installed on it because LINUX tries to update packages that you install beside the operating system packages that is installed already with the operating system initial installation.

You can update your system by using this command:

sudo apt-get udpate

The output of this command is a part of the output shown before in the section **Basic LINUX Commands** **#Image7|graphic**

You can upgrade your LINUX system using this command:

sudo apt-get upgrade

The output of this command is also a part of the output shown before in the section **Basic LINUX Commands** **#Image7|graphic**

You can upgrade your LINUX distribution (only) means that you will upgrade within the same distribution versions but not to the newest distribution using the following command:

sudo apt-get dist-upgrade

The output of this command is also a part of the output shown before in the section **Basic LINUX Commands** **#Image7|graphic**

**Of course you can get around problems while performing update, upgrade, and dist-upgrade using a key called --fix-missing and it will try to go around broken links and other update problems that it may face during the process execution.**

So basically, this is the end of part 1 LINUX Desktop, Server and Cloud Image which has added a general idea of how LINUX machine is working and how to do various tasks id different area of management of a LINUX machine.

Let’s Move Around to Part 2.

# 2 Linux Infrastructure

## 2.1 Installing DNS, DHCP, and Kerberos

Lets walk through the installation of BIND9 which is the DNS Package Name on UBUNTU

Installing BIND9 is using this command:

#### **sudo apt-get install bind9**

Running this command will give the output with confirmation as figure 2.1 shows:

![](image/Image1101.jpg)

When you press Y and hit enter key on your keyboard the installation will continue until finished and you will get to the bind configuration process to get everything up and running.

To configure bind 9 we need to run the following command:

sudo nano /etc/bind/named.conf.options

You will be editing this file, please find a line of text containing forwarders:

forwarders{

00.00.00.00;

}

Please change the number between brackets from the current IP address to your IP address. In my case, my IP address is 192.168.0.2

So the forwarders section becomes like this:

forwarders{

192.168.0.2;

}

Now, you need to enter the following command to edit another file called named.conf.local

sudo nano /etc/bind/named.conf.local

Then, what you need to do is changing adding the following entries or changing the current entries if found:

zone “manon.com” {

type master;

file “/etc/bind/db.manon.com”;

};

zone “0.168.192.in-addr.arpa” {

type master;

file “/etc/bind/db.192”;

};

Press CTRL + W to quit, confirm using Y, then hit enter on your keyboard.

Now, you need to execute the following command to copy a file using cp keyword from the original place and create your own with a suitable file name for this configuration situation:

sudo cp /etc/bind/db.127 /etc/bind/db.192

The copied file is into the path /etc/bind/db.127 and copied to /etc/bind/db.192

After Copying the file, you should edit the copied file using the following command:

sudo nano /etc/bind/db.192

After that you will be presented with the file content, edit the file content and make it suitable for your needs as follows:

;

; BIND reverse data file for local loopback interface

;

![](image/Linux_for_system_3.jpg)

You will find the area that you should edit are highlighted so you can customize it according to your needs and put into consideration that the last line is containing the number 2 at the beginning will be the last octet in your IP address.

When you finish this, you need to start copying another file using this command:

sudo cp /etc/bind/db.local /etc/bind/db.manon.com

this command is copying a file from location /etc/bind/db.local to the destination /etc/bind/db.manon.com

Do not forget to change your destination file from db.manon.com to your host name that you desire your server string will be.

After finishing this we need to edit the file db.manon.com to change its content as follows:

sudo nano /etc/bind/db.manon.com

Then you need to change the content of this file to be as follows:

![](image/Linux_for_system_4.jpg)

I have highlighted the editable areas for you to change it to your specific environment as follows:

manon.com to replace it with your host name.

192.168.0.1 to replace it with your IP v4 address.

::1 to replace it with your IP v6 address.

One more thing we need to do is:

We need to edit the content of the file /etc/default/bind9 as follows:

sudo nano /etc/default/bind9

Now, you need to search for a line called

RESOLVCONF=no

And Change the value no to yes to be like this:

RESOLVCONF=yes

This way, you need to exit the editor using CTRL + X and confirm the file changes using Y, then you need to hit enter on your keyboard to get back to the terminal.

We need to restart the service called bind9 that we have installed on the machine using this command:

sudo service bind9 restart

After restarting your service, please run this command to check whether your server is responding and up and running:

sudo dig 192.168.0.2

Please replace the number 192.168.0.2 with your IP address of the server that you are installing this DNS on it.

If you had a response like what is in the following figure 2.2:

![](image/Image1110.jpg)

Then, you have successfully installed your DNS successfully.

But if you did not see this message, please revise the section about trouble-shooting your LINUX machine in *Appendix B* ................................................................ Troubleshooting your LINUX Machine DNS

Please do not consult Appendix B before you make sure you made the previous steps exactly as requested.

Our next step will be installing DHCP on your LINUX machine as follows:

sudo apt-get install isc-dhcp-server

After running this command, you will be presented with the following output as the following figure 2.3:

![](image/Image1121.jpg)

After running the previous command, you need to make some changes in the configuration as follows:

sudo nano /etc/dhcp/dhcpd.conf

You will now edit the file by searching the content of the file for a line called

option domain-name = “example.com”;

You need to edit the contents of the file to make it like the following content starting from this file until the end of the content below:

option domain-name “manon.com”;

option domain-name-servers ns1.manon.com, ns2.manon.com;

default-lease-time 600;

max-lease-time 7200;

option subnet-mask 255.255.255.0;

option broadcast-address 192.168.0.255;

option routers 192.16.0.254;

subnet 192.168.0.0 netmask 255.255.255.0 {

range 192.168.0.80 192.168.0.100;

range 192.168.0.120 192.168.0.220;

}

I have highlighted the editable content to make it fit your environment.

The previous configuration has assigned the ranges from 80–100 to the clients of the subnet and from 120–220 to the same subnet.

What does this mean? If any computer is going to join this domain as illustrated in the figure #Image4|graphic in this book that contained the infrastructure sample of connected computers, printers, tablet, etcetera, every device of these will obtain an IP address within the ranges that you have specified in this DHCP server.

One more thing to go with the previous installation is to restart the DHCP server using the following command:

sudo service isc-dhcp-server restart

This way, we have completed installing our DHCP server on UBUNTU.

The following figure 2.4 shows the 2 installations that we did and how they relate to the network infrastructure that you are building:

![](image/Image1132.jpg)

Our LINUX distribution here will be installed on the cluster controller machine in the Data Center RAC.

Our DHCP server will be installed on this machine and its function will be to distribute the IP addresses to PCs, Big Tower PCs, and Printers that are hooked to the BUS topology network.

If you look carefully at the Data Center RAC, SAN ISCSI storage disk, which will be manageable also by the cluster controller node when installing the file server in later chapters.

Installing Kerberos on your LINUX machine will be the next step.

Kerberos is a server to process LDAP which is a light weight directory access protocol.

To install Kerberos on your machine, we will be executing this command:

sudo apt-get install krb5-kdc-ldap

You will be prompted to enter the REALM name, for example if you made your DNS name in the DNS installation step as manon.com, then the realm name will be MANON.COM capitalized.

After that, you will be prompted to enter kerberos servers and administrative servers for your realm as follows:

Kerberos Server: KRB.MANON.COM

Administrative Server: ADMIN.MANON.COM

![](image/Image1139.jpg)

**Figure 2.5** Shows the installation process of the Kerberos packages.

After the previous installation, we need to install LDAP utilities using the following command which will work as a back-end for our PHP front-end that we will install later after this installation:

sudo apt-get install slapd ldap-utils

This is containing 2 packages to install slapd and ldap-utils.

When you finish this installation we need to re-configure the package slapd by using the following command:

sudo dpkg-reconfigure slapd

After running this command, you will be presented with the following:

When prompting for omit ldap server configuration: choose no.

Please enter the DNS domain name: in my case: manon.com

When it comes to administrator password, please type in the password that you have used in the previous installation steps.

When it comes to database type to use: choose HDB

When it comes to remove database when slapd is purged: choose no

When it comes to move old database: choose yes

And finally, when it prompts to allow ldapv2 protocol: choose no

When you are finished with this:

Run the following command:

sudo apt-get install phpldapadmin

This will be the front end for our LDAP server and will be working as a user interface for managing LDAP users and groups.

After the installation finishes, we need to edit the following file using nano as follows:

sudo nano /etc/phpldapadmin/config.php

Find the entries

$servers->setValue(‘server’,’host’,’manon.com’);

The fields that you need to change according to your environment are highlighted in yellow.

You will also need to find this line:

$servers->setValue(‘server’,’base’,array(‘dc=manon,dc=com’));

And also the fields that need to change are highlighted in yellow.

The final step is to fine the following line of code to change it to the following values:

$servers->setValue(‘login’,’bind_id’,’cn=admin,dc=manon,dc=com’);

You will also find the fields that need to be edited are highlighted in yellow.

When you are finished, please open your browser and point it to the following address putting into consideration to change it according to your environment specifications:

[http://manon.com/phpldapadmin/](http://manon.com/phpldapadmin/)

![](image/Image1149.jpg)

**Figure 2.6** shows the PHP LDAP admin front-end.

After opening this screen, you will be presented with user name and password, and you need to enter the user name as follows and putting into considerations the changes in your environment:

cn=admin,dc=manon,dc=com

The fields that need to be changed are highlighted in yellow.

Now, we have completely installed our LDAP Kerberos on our DNS and remains the security part that we will come to apply it in the chapter **Security in LINUX**.

## 2.2 Managing Users and Groups

*   Adding a new user:

If you want to add a new use, please run the following command:

sudo adduser manon

You need to change manon word to the user name you will need in your environment.

It will prompt you to enter the details of the user and confirmation that these details are correct or not.

If you want to make this user as administrator and can perform all kinds of tasks on the machine, please execute the following commands as follows:

sudo visudo

You will find your self into the text editor that we had to use before and we will edit some lines as follows:

search for the line that contains the user name that you have just created in the command adduser in the terminal and change the line to the following:

manon ALL=(ALL:ALL) ALL

*   If you want to delete the user, you can use the following:

sudo deluser manon

If you want to delete the user with all the files that belong to this user on the system, then you can use the following command:

sudo deluser --remove-home manon

And then execute the same command again as follows:

sudo visudo

Then search for the line that we have added before:

manon ALL=(ALL:ALL) ALL

Then remove it or make a preceding hash sign like this

#manon ALL=(ALL:ALL) ALL

To comment it and make it useless into the file if you will use it later.

*   Creating a group

If you want to create a group, then you will need to execute this command:

sudo addgroup manonsys

This way, you have added a new group of users into your LINUX machine.

If you want to join the user into this group, then execute the following command:

sudo adduser manon manonsys

This way, we have joined the user “manon” to the group “manonsys”.

If you want to change the user privileges to access or deny access to directories (folders), files, etcetera, then you will need to go to chapter **Installing and Managing FTP, SFTP** which we will talk about file servers and managing directories and installing protocols that enable the users to communicate with the system directories.

## 2.3 Installing and Managing Linux Firewalls

Firewall is a way to protect your machine input and output by filtering it and preventing unauthorized access to any sensitive data you do not want to reveal.

To install your firewall on LINUX, you need to issue the following command on your terminal:

sudo apt-get install ufw

This command might give the package is installed already and the newest version because it might be installed with your operating system by default.

If you finished installing the package, we need to enable it by issuing the following command:

sudo ufw enable

To show the status of your firewall, you need to execute the following command:

sudo ufw status verbose

![](image/Image1156.jpg)

You will be presented with a screen like the previous 2.7 figure showing the results of the previous command.

No that we made sure that our firewall is installed, up and running.

To enable a port number on your machine, we will execute the following command:

sudo ufw allow 53

This command will enable the traffic to pass in and out on port 53.

We will also learn what are ports when working on securing your LINUX distribution, installing web servers on LINUX, and installing ssh and file servers on LINUX because every installation of these will require 1 port number or more to use within the installation.

Every service of these can be added to the rules of the firewall we are using by allowing or denying it.

![](image/Image1164.jpg)

To deny a port number, we can use the following command:

sudo ufw deny 53

This will deny port 53, and the result of the previous command will be identical the command that we issued for enabling the same port.

If you want to allow or deny a specific port with a specific protocol, you need to issue the following command:

sudo ufw allow 53/tcp

This command will make port 53 enabled for use with the TCP protocol only.

If you want to disable the same port with the same protocol, you need to need to execute the following command as follows:

sudo ufw deny 53/tcp

1 more thing to go, is if you want to enable a UDP protocol with any port, you can execute the following command:

sudo ufw allow 53/udp

And if you want to disable a UDP protocol with any port, you can execute the following command:

sudo ufw deny 53/udp

Finally, if we want to disable the firewall completely, then we need to execute the following command:

sudo ufw disable

Now, we have managed our LINUX firewall and learn how enable, disable, and manage ports to accept or deny specific protocol on a specific port number or accept or deny all port number protocols in general.

## 2.4 Installing and Managing Web Servers

Web servers are used to host websites on your machine.

If you want to install the most popular web server, then it is Apache that can serve PHP, MySQL, Java, and even Python pages.

Apache® web server is ranked #1 in the world ranking statistics of web servers, this is why we will focus on installing a server stack on our LINUX machine called LAMP.

The LAMP abbreviation stands for LINUX, Apache, MySQL, and PHP.

To install the LAMP stack on your UBUNTU LINUX machine, we will execute the following commands:

sudo apt-get install tasksel

When this execution is finished, we need to execute the command that will install the stack itself as follows:

sudo tasksel install lamp-server

This command will order tasksel that we installed before to install lamp-server package.

You will be prompted to enter the password, and confirm it for your MySQL database server.

After that, when you finish walking through the procedures of the previous command, we will install a GUI for managing our database server called PHPMyAdmin.

PHPMyAdmin is a powerful tool that is used to manage MySQL databases, execute queries, manage users and more.

To install PHPMyAdmin, we need to execute the following command as follows:

sudo apt-get install phpmyadmin

Executing the command will lead you to enter your MySQL password, please enter the same passwords that you entered when installing the LAMP server in the previous command, and you can also use the same password for the management system account.

And you can permit the PHPMyAdmin to create it own database on MySQL server by selecting yes when prompted.

This way we have installed our LAMP stack, and a web server that we can use to host applications on our UBUNTU LINUX machine.

To test our installation, we need to create a file called index.php and place this file in the following directory:

/var/www/html/

To create this file, we need to execute the following command:

sudo nano /var/www/html/index.php

This will open a text editor on the terminal window to add some text.

We need to add to following lines of code to our file as follows:

<?php

echo phpinfo();

Then we need to press CTRL + X to close the file and confirm the changes by typing “Y” and then hitting enter on the keyboard to confirm the path and file name.

After finishing all the requirements, we need to open a browser and point the address to the following URL:

[http://localhost/](http://localhost/)

This will make you see the following figure 2.9 which will contain all the server configuration settings for your PHP installation.

![](image/Image1172.jpg)

If you face any problem, please consult the *Appendix F* Troubleshooting your LINUX Web Server.

## 2.5 Installing and Managing Mail Servers

After installing our DNS, we will integrate our Mail server on this DNS as the following procedures will be about:

1.  We need to install a package called POSTFIX on our UBUNTU LINUX operating system.

    Installing this package is done by executing the following command:

    sudo apt-get install postfix

    You can simply accept the default because we will be working on re-configuring the package.

2.  We need to re-configure the package in order to apply our environment specific data as follows:

    sudo dpkg-reconfigure postfix

You will be presented with a series of screens where you need to apply your configuration settings as follows:

*   Internet Site.
*   None doesn’t appear to be requested in the current config.
*   System mail name will be manon.com and you need to change it to the domain that you have chosen when installing your DNS.
*   mostafa #adjust it to use your own user name.
*   manon.com, localhost, localhost.localdomain, localhost #adjust manon.com to your own string used when installing your DNS.
*   No.
*   192.168.0.2 #Adjust it to your own IP address.
*   Yes
*   0
*   +
*   all

Now we need to run the following series of commands 1 by 1 to continue with the configuration process:

*   sudo postconf -e ‘home_mailbox = Maildir/’
*   sudo postconf -e ‘mailbox_command =’
*   sudo postconf -e ‘smtpd_sasl_local_domain =’
*   sudo postconf -e ‘smtpd_sasl_auth_enable = yes’
*   sudo postconf -e ‘smtpd_sasl_security_options = noanonymous’
*   sudo postconf -e ‘broken_sasl_auth_clients = yes’
*   sudo postconf -e ‘smtpd_recipient_restrictions = permit_sasl_authenticated,permit_mynetworks,reject_unauth_destination’
*   sudo postconf -e ‘inet_interfaces = all’
*   sudo apt-get install postfix-tls sasl2-bin libsasl2 libsasl2-modules
*   sudo nano /etc/default/saslauthd
*   Add or change the following:
*   START=yes
*   MECHANISMS=”pam”
*   sudo nano /etc/postfix/sasl/smtpd.conf
*   Add the following:
*   pwcheck_method: saslauthd
*   sudo nano /etc/postfix/main.cf
*   Add the following data:
*   smtpd_sasl_auth_enable = yes
*   smtpd_sasl_security_options = noanonymous
*   broken_sasl_auth_clients = yes
*   smtpd_recipient_restrictions = permit_sasl_authenticated, permit_mynetworks, reject_unauth_destination
*   sudo rm -r /var/run/saslauthd/
*   sudo mkdir -p /var/spool/postfix/var/run/saslauthd
*   sudo ln -s /var/spool/postfix/var/run/saslauthd /var/run
*   sudo chgrp sasl /var/spool/postfix/var/run/saslauthd
*   sudo adduser postfix sasl
*   sudo service postfix restart
*   sudo service saslauthd restart
*   sudo nano /etc/postfix/sasl/smtpd.conf and add the following details
*   pwcheck_method: saslauthd
*   mech_list: plain login
*   touch smtpd.key
*   chmod 600 smtpd.key
*   openssl genrsa 1024 > smtpd.key
*   openssl req -new -key smtpd.key -x509 -days 3650 -out smtpd.crt
*   openssl req -new -x509 -extensions v3_ca -keyout cakey.pem -out cacert.pem -days 3650
*   sudo mv smtpd.key /etc/ssl/private/
*   sudo mv smtpd.crt /etc/ssl/certs/
*   sudo mv cakey.pem /etc/ssl/private/
*   sudo mv cacert.pem /etc/ssl/certs/
*   sudo postconf -e ‘smtp_tls_security_level = may’
*   sudo postconf -e ‘smtpd_tls_security_level = may’
*   sudo postconf -e ‘smtpd_tls_auth_only = no’
*   sudo postconf -e ‘smtp_tls_note_starttls_offer = yes’
*   sudo postconf -e ‘smtpd_tls_key_file = /etc/ssl/private/smtpd.key’
*   sudo postconf -e ‘smtpd_tls_cert_file = /etc/ssl/certs/smtpd.crt’
*   sudo postconf -e ‘smtpd_tls_CAfile = /etc/ssl/certs/cacert.pem’
*   sudo postconf -e ‘smtpd_tls_loglevel = 1’
*   sudo postconf -e ‘smtpd_tls_received_header = yes’
*   sudo postconf -e ‘smtpd_tls_session_cache_timeout = 3600s’
*   sudo postconf -e ‘myhostname = manon.com’ # You need to change this to your host name.

    Finally we need to restart POSTFIX service using the following command:

sudo service postfix restart

Next, we need to install the following packages to complete the security of our POSTFIX mail Server as follows:

sudo apt-get install libsasl2-2 sasl2-bin libsasl2-modules

Next, we need to edit the following values in a file */var/spool/postfix/var/run/saslauthd*

sudo nano */var/spool/postfix/var/run/saslauthd*

Remove the hash # sign before the line START=yes

Add the following lines next to the previous line that we have edited now as follows:

PWDIR=”/var/spool/postfix/var/run/saslauthd”

PARAMS=”-m ${PWDIR}”

PIDFILE=”${PWDIR}/saslauthd.pid”

After that we need to change the OPTIONS line at the end of the file to be:

OPTIONS=”-c -m /var/spool/postfix/var/run/saslauthd”

Next we need to execute the following commands:

sudo dpkg-statoverride --force --update --add root sasl 755 /var/spool/postfix/var/run/saslauthd

If the previous command produces a warning or error, ignore the error because the directory reported will be created automatically in the next steps.

Next, we need to execute the following command:

sudo ln -s /etc/default/saslauthd /etc/saslauthd

Finally, we need to restart our service:

sudo service saslauthd restart

To test our installation, we need to execute the following command:

telnet localhost 25

OR

telnet manon.com 25 # Replacing manon.com with your own DNS string.

Then execute the following command after your connection starts:

ehlo localhost

OR

ehlo manon.com

This way, we have completed our installation or our mail server and let us integrated into our LAMP Web Server and Send our First HTML formatted Web Mail.

Execute the following command to edit the PHP.ini configuration file as follows:

sudo nano /etc/php5/apache2/php.ini

Search in the file for an entry called sendmail_path and change it to sendmail_path = "/usr/sbin/sendmail -t -i"

Now execute the following command to create a file called sendMail.php to send your first mail using the following command:

sudo nano /var/www/html/sendMail.php

Enter the following content into your file as follows:

<?php

$to = “mailofpersontosendto@hotmail.com, **anothermailtosendto@gmail.com**”;

$subject = “HTML Mail Subject”;

$message = “

<html>

<head>

<title>Title of the E-Mail</title>

</head>

<body>

<p>This is an HTML E-Mail Message !!!</p>

<table>

<tr>

<th>Column 1 Header</th>

<th>Column 2 Header</th>

</tr>

<tr>

<td>Content of Column 1 in HTML E-Mail</td>

<td>Content of Column 2 in HTML E-Mail</td>

</tr>

</table>

</body>

</html>

“;

$headers = “MIME-Version: 1.0” . “\r\n”;

$headers .= “Content-type:text/html;charset=UTF-8” . “\r\n”;

$headers .= ‘From: mostafa@manon.com’ . “\r\n”;

$headers .= ‘Cc: manonmanager@manon.com’ . “\r\n”;

if(mail($to,$subject,$message,$headers)){

echo ‘Mail have been send successfully as desired.’;

}else{

echo ‘We have encountered some error, please consult <br />*Appendix G* Troubleshooting your LINUX Mail Server’;

}

Now point your browser to the following URL:

http://manon.com/sendMail.php

OR

http://localhost/sendMail.php

After visiting this URL, you will be noticed if the mail message has been sent or not.

If you experienced any error, please consult:

*Appendix G* Troubleshooting your LINUX Mail Server

Now, we have completely installed LINUX mail server and you can enjoy sending mails.

## 2.6 Installing and Managing FTP, SFTP

Let us try installing our file server. Installing your file server will make you have access to save, update, and delete file within your machine using FTP, SFTP protocols as follows:

sudo apt-get install vsftpd

When finishing your installation, please run the following command to configure your FTP server settings:

sudo nano /etc/vsftpd.conf

When finished, edit the following lines and make it identical:

anonymous_enable=NO

local_enable=YES

write_enable=YES

chroot_local_user=YES

Save and Exit by Pressing CTRL + X, and then Press Enter Key on Your Keyboard.

Now, create a directory as follows:

sudo mkdir /home/manon/files #changing manon with your operating system’s user name.

Then, we need to change ownership of the

sudo chown root:root /home/manon

#changing manon with your operating system’s user name

Now, we need to restart the service by executing the following command:

sudo service vsftpd restart

Now, connect to your FTP server by executing the following command from the terminal as follows:

sudo ftp localhost

We use the user name of the operating system that we have used while doing the previous tasks, then we put the password of that account.

When finished, type exit on the terminal to terminate your ftp session.

Now, let us install the FTP client application as follows:

sudo apt-get install filezilla

When installed, start your filezilla application and put in the host field: [ftp://manon.com/](ftp://manon.com/)

User Name: manon

Password: *******

When finished, click connect and now, you have connected to your file server.

You can create directories on your server, create files, and manage it.

Now, let us map a network drive on a Windows® machine as follows:

Open start menu and type map network drive in the search box.

In the location field, type the FTP server name which is [ftp://manon.com/](ftp://manon.com/)

When prompted, type the user name and password we just mentioned earlier.

To install the secured layer of FTP which is SFTP, we need to execute the following command:

sudo a2ensite default-ssl.conf

Then we need to execute the command:

sudo service apache2 restart

Then, we need to install ssh as follows:

sudo apt-get install ssh

After finishing the installation, we will be able to connect to the server using SFTP using the URL:

sftp://manon.com # changing manon.com with your DNS name.

Now, let us connect to FTP and SFTP using our tablet device as follows:

I will use an iOS enabled tablet device to and browse store applications on Apple® app store and find an application called FTPManager Free®.

After installing your application on your iPad or iPhone, you will find a + sign at the main menu of the application used to add a server connection

Type the server address [ftp://manon.com](ftp://manon.com/) or [sftp://manon.com/](sftp://manon.com)

Choose the protocol ftp or sftp

Type the user name and password for your ftp account at the bottom.

You are now connected to your file server and you are ready to move, and add files to your server.

You can also download files from the server as needed.

Now, we covered working with our file server installation, configuration and management.

## 2.7 Installing and Configuring SAMBA and Managing Shares

SAMBA is another way to install a file server. To install SAMBA, we need to go through the following steps:

sudo apt-get install samba

sudo nano /etc/samba/smb.conf

Add the following lines at the end of the file:

[share]

comment = Ubuntu File Server Share

path = /srv/samba/share

browsable = yes

guest ok = yes

read only = no

create mask = 0755

Execute the following commands to create the share directory:

sudo mkdir -p /srv/samba/share

When finished, give the shared directory suitable permissions as follows:

sudo chown nobody:nogroup /srv/samba/share/

Execute the following command to apply changes of configuration:

sudo service smbd restart

sudo service nmbd restart

This way, we have configured and installed our SAMBA File Server and Created a Share, so if you browse any Windows OS machine network tab to browse the computers of the network, you will find that our server’s share appears to all windows users.

## 2.8 Installing GIT Server

You got a project and you want to create a local GIT server instead of pushing to the public GIT control systems, here is a solution to create your own git server so you can push your project locally on your machine with your team members.

Execute the following commands:

sudo apt-get install git

When finished running the installation, execute the following command:

git config --global user.email “[mostafa@manon.com](mailto:mostafa@manon.com)”

After that, we need to assign a user name for anyone to connect to the machine using it as the following command:

git config --global user.name “mostafa”

Now let us create our first repository by adding our web directory that has been created when we installed our web server by executing this command:

git init --bare /var/www/html/

If you face any problems with the previous command, you need to issue the following command instead

cd /var/www/html/ && git init .

Now we do clone to the repository using our user name and password

git clone [mostafa@localhost](mailto:mostafa@localhost):/var/www/html/

Then, we need to execute the following command:

cd /path/to/repository

Then we make something called commit and give a message to it or leave it blank as follows:

git commit -a

or

git commit -m “Contents are Finished”

Then we push any changes to the repository as follows:

git push origin master

Installing another GIT Server:

There is another git server that performs the same functionality as the previous GIT server that we have installed. Lets walk through the installation of this server as follows:

sudo apt-get install gitolite

When finished, add a new user to the system called GIT by executing the following command as follows:

sudo adduser --system --shell /bin/bash --group --disabled-password --home /home/git git

Now we need to consult installing SSH server and client on your machine article and follow the following commands:

ssh-keygen -t rsa

Accept defaults and just hit enter on your keyboard until finished, then execute the following command:

cp ~/.ssh/id_rsa.pub /tmp/$(whoami).pub

Then, we need to login to the user that we have created using the following command:

sudo su - git

gl-setup /tmp/*.pub

Now, you need to exit the session of the user that we logged in by executing the following command:

exit

After all, we need to clone to the repository as follows:

git clone git@manon.com:gitolite-admin.git

All what you need to do is: To change the manon.com with your computer’s DNS name as you chose when installing your DNS server which is highlighted in yellow.

Now you can browse the content of the project using the following commands:

cd gitolite-admin

ls -l

To add the repository to an existing project, you can execute the following command as follows:

git remote add gitolite git@$manon.com:manonproject.git

Now, we have finished installing, configuring, and using our GIT server and client.

# 3 Security in Linux

## 3.1 Installing SSH

SSH server is used to connect to your machine using secured socket layer with encryption mechanisms like using key pairs for private and public.

The concept of private and public key pairs are for use as follows:

The private key stays on the destination machine in a standard encryption format and usually SHA-256 encryption mechanism alongside with SHA-2 and RSA which is the basic encryption mechanisms.

To install your SSH server, follow the next steps:

sudo apt-get install openssh-server

Next, we install openssh-client for complete client functionality.

sudo apt-get install openssh-client

To generate key-pairs, we need to issue the following commands:

ssh-keygen -t rsa

ssh-copy-id mostafa@manon.com

Then we give enough privileges to our keys directory to make sure that everything is secured.

chmod 600 .ssh/authorized_keys

If you want to access your shell using a web browser, we need to install the following package and make some edits and configurations as follows:

sudo apt-get install ajaxterm

sudo sed -i ‘s:PasswordAuthentication.*:PasswordAuthentication yes:’ /etc/ssh/sshd_config

Next, we restart our service using the following command:

sudo service ssh restart

Now, open your browser and point to your machine using the following URL as follows:

[http://manon.com:8022](http://manon.com:8022/)

#replacing manon.com with your own IP, or DNS String that you used on your DNS installation machine, and you can also use localhost instead.

Type in your user name, then hit enter key on your keyboard.

Type In your password and hit enter key on your keyboard.

You of course enter the user name and password of your own operating system’s.

The following figure 3.1 shows the outcome of the previous installation.

![](image/Image1181.jpg)

## 3.2 Creating Certificates using SSL

In the next section, we will go through creating self signed certificates and signing it.

We will also walk through self signing your certificates and attaching your certificates with your web server as an example of using these certificates as follows:

We need to execute the following command to create a key as follows:

openssl genrsa -des3 -out server.key 2048

Note that server.key can be changed to any file name that you have used.

Now we assign RSA enctryption to our key file and put the result out to an insecure file as follows:

openssl rsa -in server.key -out server.key.insecure

Now we create our secure key as follows:

mv server.key server.key.secure

Then we move the key as follows:

mv server.key.insecure server.key

Now, we create certificate signing request using the following command:

openssl req -new -key server.key -out server.csr

Now, submit all the files to a signing authority like Comodo® as an example of a certificate signing issuing organization on the following URL:

[https://www.instantssl.com/free-ssl-certificate.html](https://www.instantssl.com/free-ssl-certificate.html)

Complete the wizard, submit your certificate key, verify your DNS by hosting the requested file over HTTP or HTTPS, and also there are several other options to do that.

Create a self signed certificate as follows:

openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

sudo cp server.crt /etc/ssl/certs

sudo cp server.key /etc/ssl/private

sudo mkdir /etc/ssl/CA

sudo sh -c “echo ‘01’ > /etc/ssl/CA/serial”

sudo touch /etc/ssl/CA/index.txt

After running the previous commands which is creating key files and related directories, we need to edit in the configuration of our operating system openssl package configuration file as follows:

sudo nano /etc/ssl/openssl.cnf

We need to find the following values and edit them carefully as follows:

dir = /etc/ssl/

database = $dir/CA/index.txt

certificate = $dir/certs/cacert.pem

serial = $dir/CA/serial

private_key = $dir/private/cakey.pem

If you made changes to the files names that we created above in the previous commands, you also need to apply the same changes to this configuration file to be in parallel.

Now, we need to request the the self signed root certificate as follows:

openssl req -new -x509 -extensions v3_ca -keyout cakey.pem -out cacert.pem -days 3650

Also, we need to move the key files the default directory as follows:

sudo mv cakey.pem /etc/ssl/private/

sudo mv cacert.pem /etc/ssl/certs/

Now we sign the certificate as follows:

sudo openssl ca -in server.csr -config /etc/ssl/openssl.cnf

Now there is a new file in the following directory called /etc/ssl/newcerts/01.pem, we need to rename this file to our needs and move it to the following directory with the new name as follows:

sudo mv /etc/ssl/newcerts/01.pem /etc/ssl/certs/manon.com.pem

Now, we need to configure our https server to use this certificate that we have created using the following:

sudo nano /etc/apache2/sites-available/default-ssl.conf

Let’s search and edit the entries as follows:

SSLCertificateFile /etc/ssl/certs/manon.com.pem

SSLCertificateKeyFile /etc/ssl/private/server.key

When we edit the file it will be looking much like the following figure 3.2 as follows:

![](image/Image1188.jpg)

Now we can press CTRL + X to close this screen and press enter key on the keyboard to save everything.

When finished, we need to restart our apache server by issuing the following command as follows:

sudo service apache2 restart

During the previous process, there would be some prompts, like passwords, country names, user file names, and city and state values. You can of course use your own values, or the values specific for your needs.

When you are finished with everything, you browse your [https://manon.com](https://manon.com/) server and confirm your security exception to add the website to the trusted sites, click on the little icon beside the address [https://manon.com/](https://manon.com/) directly and you will find that a windows opens to you, click on more information, then go to the security tab if not enabled by default and then click view certificate, then you will find that the certificate is populated with your protocol with the server name manon.com as you will see in the following figure 3.3 as follows:

![](image/Image1196.jpg)

## 3.3 Working with SELinux and Access Control

SELINUX is a gateway to enable and disable services and control port number and access through your system.

To install SELINUX on UBUNTU LINUX machine, we use the following command:

sudo apt-get install selinux

There are 2 main options to configure SELINUX packages, we will mention them with how to enable each one of them as follows:

*   Permissive: manon.comMost popular option and the command to enable this option is:

    sudo sed -i ‘s/SELINUX=.*/SELINUX=permissive/’ /etc/selinux/config

*   Enforcing: The most secure option and the command to enable this option is:

    sudo sed -i ‘s/SELINUX=.*/SELINUX=enforcing/’ /etc/selinux/config

Another firewall package that is already installed by default on UBUNTU is:

UFW

UFW is installed by default as we said and we will go through its configuration and manipulation commands as follows:

To enable the service, we need to run the following command:

sudo ufw enable

To enable or disable a port on one of the services you are using like HTTP or HTTPS, we need to issue toe following commands

sudo ufw allow 8080 #Enable HTTP port 8080

sudo ufw allow 80 #Enable HTTP port 80

The previous port number 8080 and 80 are the mainly used port numbers by UBUNTU for HTTP protocol. If you disabled one of these ports, you will not be able to browse your [http://localhost/](http://localhost/) or [http://manon.com/](http://manon.com/) from other machines.

sudo ufw deny 8080 #Disable HTTP port 8080

sudo ufw deny 80 #Disable HTTP port 80

sudo ufw allow 22 #Enable HTTPS on port 22

sudo ufw deny 22 #Disable HTTPS on port 22

You can also delete a rule that you have created as follows:

sudo ufw delete deny 22

sudo ufw delete deny 80

sudo ufw delete deny 8080

You can also call allow, deny services by service name using the following command:

sudo ufw deny http

sudo ufw deny https

sudo ufw deny Samba

Finally, we can enable and disable the service using the following command:

sudo service ufw start

sudo service ufw stop

sudo service ufw restart

## 3.4 Connecting to Linux Machine

In the next section, we will learn hot to connect to your LINUX machine using SSH protocol as follows:

ssh localhost

We use this command to connect to the machine locally within our local network.

If we obtained a static IP address service from our service provider and applied it to our LINUX connection, we will be able to connect to our machine anywhere using the following command:

ssh 192.168.0.2

Replacing 192.168.0.2 with your ISP IP address that you will gain.

You can also connect to your machine using the DNS string that we used while working on installing your DNS on your UBUNTU LINUX machine as follows:

ssh manon.com

You will need a user name and a password to access the machine and if you have a public – private key pairs installed like we mentioned in #Creating Certificates using SSL section that was containing your key files that we created.

To use a key file, we need to issue the following command:

ssh -l mostafa -i /etc/ssl/certs/manon.com.pem manon.com

OR

ssh -l mostafa -i /etc/ssl/certs/manon.com.pem localhost

Enter the pass pharase that you used while creating your file.

Enter the operating system’s password that you use to login to the system.

And, you will be presented with the following screen as in figure 3.4.

![](image/Image1205.jpg)

This way you can fully control your machine remotely and perform any task on it.

We have now covered the topic on how to connect to your machine using SSH service.

## 3.5 Securing your Web Server in Linux

To secure your web server in LINUX, we need to review a checklist that we will go through when landing to the topic web server security as follows:

1.  Perform connection using different methodologies that we mentioned earlier in previous topic while connecting to your LINUX machine without the use of any passwords or key files and attempt to create an anonymous connection to your machine.
2.  Perform an HTTP and HTTP scanning using one of the following tools:

    Httrack

    Burp Suite

    Web Scarab

    You can search the web also for HTTP scanning tools and perform a scan on your machine as a target.

    There are also online scanning tools that you can use on your browser.

3.  Use .htaccess file when deploying your applications as follows:

    Disable indexing your directories and do not permit the users from seeing directory contents by executing the following command:

    sudo nano /var/www/html/.htaccess

    Add the following line of code to the file that we have created as follows:

    Options -Indexes

    Save the file using CTRL + X and then confirm the file location and same file name by pressing enter key on your keyboard.

    When you finish try opening an empty directory in your web server, and you will end up with an error of permission denied notice page on the web browser.

## 3.6 Securing your Database Server in Linux

To secure your database server that we have installed which is MySQL server, we need to do the following installations and configurations as follows:

Enter the following command:

mysql_secure_installation

Enter the root password that we used when installing database server or LAMP server when prompted.

In the change root password prompt, you can change it or not according to your environment by typing Y or N as Yes or No options.

In the remove anonymous users prompt, type Y and hit enter.

In the disallow root login remotely select Y for the sake of security, just not to let someone from another machine even on the same network to login to the database server.

In the remove test database and access to it prompt, select Y and hit enter.

In the reload privilege table now, select Y and hit enter.

![](image/Image1216.jpg)

Noice that, you will be presented at the end of our configuration with the following screen as figure 3.5.

But notice that in my state, I have allowed my remote login attempt to make the server available for accessing it remotely and this option will be recommended for Cloud Image installation, if you are using UBUNTU in a cloud environment, then you will use this option because you will be connecting to your database server remotely.

## 3.7 Securing your Linux Virtual Machine

Securing your LINUX virtual machine is exactly like security your LINUX machine except putting into consideration that the virtual machine is being accessed remotely. So, when working with the security measurements, you need to put into consideration the public access more than its local access.

# 4 Networking in Linux

## 4.1 Wired Networking in Linux

There are several ways to work with networking in LINUX. Networking is divided into wired, wireless and cellular connections.

We will walk through wired and wireless standards only in the scope of this book due to the variations in the standards of the cellular connections and supportability on LINUX infrastructure.

To list the interfaces (network adapters) that are currently available on your machine, we can execute the following command as follows:

ls /sys/class/net

![](image/Image1227.jpg)

**Figure 4.1** shows the output of listing the interfaces command.

We can also get a list of the currently available network interfaces using the following command which will give us more details about every interface.

ip addr

![](image/Image1234.jpg)

**Figure 4.2** Shows the output of listing the interfaces in more details.

Now, we need to configure our network adapters as follows:

sudo vi /etc/network/interfaces

If you want to configure you network adapter to use a static IP address, then we need to add the following lines to the file that we are editing as follows:

auto eth0

iface eth0 inet static

address 192.168.0.2

netmask 255.255.255.0

network 192.168.0.1

broadcast 192.168.0.255

gateway 192.168.0.1

dns-nameservers 192.168.0.1

![](image/Image1242.jpg)

**Figure 4.3** shows the configuration settings above that we have to apply to our network adapter.

Then we need to restart the networking as follows:

sudo ifdown -a && sudo ifup -a

This way, we have configured our wired networking adapter to use a static IP address that we assigned.

## 4.2 Wireless Networking in Linux

To start working with your wireless network adapter, we need to list the adapters to get to know the adapter name that we will use by executing the following command:

sudo ls /sys/class/net

Or in more details, we can issue the following command as follows:

ip addr

In my case the wireless adapter name is called wlan0

In most systems on LINUX machines, this is the default name for the wireless adapter that you work with, and if you have installed more that one adapter to your machine, you will find them named wlan1, wlan2, wlan3, etcetera.

We need to issue the following command to get to edit our networking interfaces and adjust an static IP address as follows:

sudo vi /etc/network/interfaces

Now we edit the file by adding these lines of configuration as follows:

auto wlan0

iface wlan0 inet static

address **192.168.0.2**

netmask 255.255.255.0

network 192.168.0.2

broadcast 192.168.0.255

gateway **192.168.0.2**

dns-nameservers **192.168.0.2**

Now press CTRL + X to save the file, confirm using the same path and name.

Now we need to restart the network adapter as follows:

sudo ifdown -a && sudo ifup -a

Or we can use the following:

sudo service network-manager restart

Or

sudo service NetworkManager restart

## 4.3 Network Manager in Linux

To manage your network manager we need to do the following:

sudo service network-manager start

sudo service network-manager stop

sudo service network-manager restart

sudo service NetworkManager start

sudo service NetworkManager stop

sudo service NetworkManager restart

The first 3 commands are used to start, stop, then re-start the service in some UBUNTU LINUX distributions and FEDORA distributions.

The last 3 commands are used to start, stop, then re-start the service in some other UBUNTU distributions only.

If you are using cloud images in UBUNTU or FEDORA, or what ever the distribution you are using is, you can install the network manager service as follows:

sudo apt-get install network-manager

To install the indicator on GNOME distributions, you can use the following command as follows:

sudo apt-get install network-manager-gnome

## 4.4 Monitoring Your Network in Linux

If you want to install bandwidth monitoring tool, we will go through the installation of bandwidthd with graphs as follows:

sudo apt-get install bandwidthd

When you finish, we need to link the installation to our web server as follows:

sudo ln -s /var/lib/bandwidthd/htdocs /var/www/bandwidth

We can restart the apache service after all to complete the process as follows:

sudo service apache2 restart

When finished, we have everything now working by pointing to the following URL:

[http://manon.com/bandwidthd/](http://manon.com/bandwidthd/)

![](image/Image1249.jpg)

**Figure 4.4** shows the console of the network bandwidth monitoring tool.

## 4.5 Scanning Your Network in Linux

1st thing that we need to do is to know what is port scanning and IP scanning on the network as follows:

Port scanning is a way to know what are the opened ports for every device that we perform the scan on.

IP scanning, is a way to know what are the IP addresses that are up and running on my network.

This is done as follows:

We need to install nmap service protocols on your UBUNTU LINUX machine as follows:

sudo apt-get install nmap

When finished, we need to perform IP scanning on the network to know which devices are connected to it as follows:

To scan a range of IP addresses in your network, we need to execute the following command as follows:

sudo nmap -sP 192.168.0.0-255

The ranges that we assigned to the scanner is as follows:

192.168.0.0

192.168.0.1

192.168.0.2

192.168.0…

192.168.0.255

Now, we have an output like what we see in the next figure 4.4.

![](image/Image1257.jpg)

Next, we need to check what are the opened ports on each host as follows:

sudo nmap -O 192.168.0.1-254

When finished, we get an output like the following:

![](image/Image1265.jpg)

Now, we can monitor the network and subnet bandwidth, scan network hosts by IP range and get the details of every host connected to network.

# 5 Private Cloud in Linux

## 5.1 Installing Openstack Services

*Openstack is cloud operating system created by a company called Redhat which is one of the leading companies in the world for the production of software and specially LINUX operating systems, LINUX services and applications.*

*One of the products that has a big market share in the cloud computing industry. Most of today’s companies and possibly the most of the biggest companies in the cloud services providers like Canonical, IBM, Redhat, Rackspace, Dell, HP, CISCO, Cloud Scaling, Poston, SUSE, Nebula, and VMWare which is nearly the ranking #1 cloud operating system in the world.*

*Let us walk through the installation of openstack using a management tool called devstack.*

*To start our installation let us type in the following command as follows:*

*If you did not walk through the installation of GIT, please go the section called installing git client and install git to get this command working with you.*

*sudo git clone* [https://git.openstack.org/openstack-dev/devstack](https://git.openstack.org/openstack-dev/devstack)

*When it finishes downloading, you need to change the permissions of your download as follows:*

*sudo chmod 777 -R ~/devstack*

*When finished, we need to start our installation as follows:*

*cd ~/devstack*

*Then we start the installation script as follows:*

*./stack.sh*

*When prompted enter the same password that you used when you installed your LAMP server. Or if you did not install any database servers, you can use any new password and recommended to be of letters and*  *numbers.*

*After all, we need to walk through a series of downloads and installation procedures done automatically with the execution of this script, then we finish up with a screen like follows:*

![](image/Image1274.jpg)

**Figure 5.1** shows the confirmation screen containing the URL of the service and credentials (user name and password)

*When finished, you will be presented with the screen containing how to access the services that we have installed as the previous figure is telling.*

Now open your browser and point to the any of the following URLs:

[http://](http://manon.com/auth/login/?next=/)[manon.com](http://manon.com/auth/login/?next=/)[/auth/login/?next=/](http://manon.com/auth/login/?next=/)

[http://](http://manon.com/auth/login/)[manon.com](http://manon.com/auth/login/)[/auth/login/](http://manon.com/auth/login/)

[http://](http://manon.com/)[manon.com](http://manon.com/)[/](http://manon.com/)

*You need to change the following previous URL domain name to your DNS string or you can use localhost or your IP address if you are using the same machine.*

*On the home screen, you will be presented with the following screen as figure 5.2 shows:*

![](image/Image1281.jpg)

*If you finished typing your user name which is demo or admin and your password as entered during installation, and you click on connect, you will be presented with the dashboard.*

*This way, we have installed our openstack services completely and functional.*

## 5.2 Working with Openstack Keystone

First thing we will learn about keystone is the authentication and authorization.

We will create a project, user name and password, create a role, and add the user to the role as follows:

To create a project using the terminal type in the following command:

sudo openstack project create --description ‘New Project’ --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin manon

You will end up with a screen like the following figure 5.3

![](image/Image1289.jpg)

To create a user using the terminal type in the following command:

sudo openstack user create --project admin --password PASSWORDHERE manon --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

When running this command, we will be presented with the following screen of confirmation as the following figure 5.4:

![](image/Image1298.jpg)

This way we have created a new user into our openstack service and we can now login in with the new credentials that we have created.

Point your browser to the previous URL as follows:

[http://localhost/](http://localhost/)

[http://manon.com/](http://manon.com/)

[http://127.0.0.1/](http://127.0.0.1/)

Then fill in the user name and password that you have used in the previous command and you are good to go.

To disable the user, we can execute the following command:

sudo openstack user set manon --disable --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

To list users, we can execute the following command:

sudo openstack user list --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

![](image/Image1309.jpg)

**Figure 5.5** shows the users that we have including the user that we have created highlighted in black background color.

To enable the user that we have disabled, we need to execute the following command as follows:

sudo openstack user set manon --enable --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

To delete a user, we can execute the following command as follows:

sudo openstack user delete manon --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

To create a role, we can execute the following command as follows:

sudo openstack role create rolename --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

![](image/Image1322.jpg)

**Figure 5.6** show the output of the previous command as follows:

To add the user to the role, we can execute the following command:

sudo openstack role add --user manon --project manon manonrole --os-username=admin --os-password=INSTALLATIONPASSPHRASE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

The output of the previous command is the same as the output of the figure 5.6.

To disable a project, you can execute the following command as follows:

sudo openstack project set manon --disable --os-username=admin --os-password=INSTALLATIONPASSPHRASE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

To enable a project, you can execute the following command as follows:

sudo openstack project set manon --enable --os-username=admin --os-password=INSTALLATIONPASSPHRASE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

To update the name of the project, we can execute the following command:

sudo openstack project set manon --name manonnew --os-username=admin --os-password=INSTALLATIONPASSPHRASE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

To show the details of a project, we can execute the following command as follows:

sudo openstack project show manonnew --os-username=admin --os-password=INSTALLATIONPASSPHRASE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

To delete a project, we can execute the following command as follows:

sudo openstack project delete manonnew --os-username=admin --os-password=INSTALLATIONPASSPHRASE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

We can also use the same commands that we have used now to edit a project against editing users and roles with the same keys that we have used in the previous commands like –os-username –os-password –os-auth-url and –os-project-name

These keys are mandatory and must be used within your commands execution procedure or can be stored in a file under each other and load that file into the terminal window and execute the commands without the need to assign these values every command execution.

This can be done as follows:

touch adminrc

sudo nano adminrc

OS_USERNAME=manon

OS_PASSWORD=password

OS_AUTH_URL=[http://localhost:5000/](http://localhost:5000/)

OS_PROJECT_NAME=admin

You have to press CTRL + X to exit the text editing screen and confirm the file path, and name by hitting the enter key on your keyboard.

Then execute the following command before executing any other commands that we have listed above as follows:

source adminrc

Then you need to execute the command as an example after sourcing the adminrc script that we have created as follows:

openstack project set manon --name manonnew

Now, we have completed the administration procedures of Openstack identity services called keystone.

## 5.3 Working with Openstack Heat

Let us get to know about Openstack Heat, Heat is the orchestration engine that is used to orchestrate openstack services and we will now get to know what are its capabilities and what can it do for our private cloud environment.

Now, we need to install heat orchestration services as follows:

Login to mysql server as a root user as follows:

sudo mysql -uroot -p

Then you need to enter the password that we have entered when installing your LAMP server, or when installing MySQL database server or when installing devstack that we walked through in the previous steps.

After that, you will be presented with the following screen as follows:

When finished, we need to create a new database called heat and grant access to it as follows:

![](image/Image1329.jpg)

CREATE DATABASE heat;

GRANT ALL PRIVILEGES ON heat.* TO ‘heat’@’localhost’ IDENTIFIED BY ‘INSTALLATIONPASSHERE’;

GRANT ALL PRIVILEGES ON heat.* TO ‘heat’@’%’ IDENTIFIED BY ‘INSTALLATIONPASSHERE’;

Now, type exit and you will find confirmation of bye message.

Next, we create a user that we will delegate the heat orchestration services to as follows:

sudo openstack user create --project admin --password PASSWORDHERE heat --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

After that, we need to create the heat service as follows:

sudo openstack role add --user heat --project manon manon --os-username=admin --os-password=INSTALLATIONPASSPHRASE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

After all, we need to create 2 endpoints that will be needed when working with Heat API.

Endpoint is a place where integration gateway works between 2 services or more, or used to communicate with a system from another.

The first endpoint we create is heat for the heat user and heat role that we have created as follows:

sudo openstack endpoint create --publicurl http://192.168.0.2:8004/v1/fc38a412004b4664a55fd9a975e40085 --internalurl http://192.168.0.2:8004/v1/fc38a412004b4664a55fd9a975e40085 --adminurl http://192.168.0.2:8004/v1/fc38a412004b4664a55fd9a975e40085 --region regionOne --os-username=admin --os-password=manon1982 --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin heat

The 2nd Endpoint that we need to create is heat-cfn

sudo openstack endpoint create --publicurl http://192.168.0.2:8004/v1/83dace3c2f44444fb8780576f341b64d --internalurl http://192.168.0.2:8004/v1/83dace3c2f44444fb8780576f341b64d --adminurl http://192.168.0.2:8004/v1/83dace3c2f44444fb8780576f341b64d --region regionOne --os-username=admin --os-password=manon1982 --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin heat-cfn

Next, we perform the following installations as follows:

sudo apt-get install heat-api heat-api-cfn heat-engine python-heatclient

Next, we need to make configuration changes to a file called heat.conf as follows:

sudo nano /etc/heat/heat.conf

We need to change the following variables according to our environment as follows:

In the database section [DATABASE]

We need to change the following line

connection = mysql://heat:HEAT_DBPASS@controller/heat

Then, we need to change the following in the section [DEFAULT]

rpc_backend = rabbit

rabbit_host = localhost

rabbit_password = guest

heat_metadata_server_url = http://localhost:8000

heat_waitcondition_server_url = http://localhost:8000/v1/waitcondition

Then we need to change the following in the section called [keystone_authtoken]

auth_uri = http://localhost:5000/v2.0

identity_uri = http://localhost:35357

admin_tenant_name = admin

admin_user = heat

admin_password = PASSWORDHERE

Then, we need to edit the following line in the section called [ec2authtoken]

auth_uri = http://localhost:5000/v2.0

Then, we need to populate our database by executing the following command:

sudo su -s /bin/sh -c “heat-manage db_sync” heat

Then, we finalize our solution by executing the following command as follows:

sudo service heat-api restart

sudo service heat-api-cfn restart

sudo service heat-engine restart

If you are using UBUNTU LINUX, then we need to issue the following command to remove unused database as follows:

rm -f /var/lib/heat/heat.sqlite

To create a stack, we need to create a file called heatorchestrationtemplate.yaml

We need to execute the following command as follows:

touch heatorehcstrationtemplate.yaml

Then we edit the file using this command:

nano heatorchestrationtemplate.yaml

After all, we need to add the following content to the file and considering any changes according to our environment as follows:

heat_template_version: 2013-05-23

description: Simple template to deploy a single compute instance

resources:

my_instance:

type: OS::Nova::Server

properties:

image: /path/to/image/downloaded_ubuntu_cloud_image.img

flavor: m1.small

key_name: keyfile.pem

networks:

- network: network-name

Then we need to adjust the data highlighted to fit our environment.

After all, we can use our file in the following command to create a heat orchestration stack as follows:

sudo openstack stack create manon_stack -f heatorchestrationtemplate.yaml

Now, we have installed our heat services, made a complete configuration to make it work properly and created a sample stack on the heat service.

## 5.4 Working with Openstack Swift

Now, let us install swift storage service and enable replication as follows:

sudo apt-get install swift swift-account swift-container swift-object xfsprogs

Now, let us create a file called rsyncd.conf as follows:

sudo nano /etc/rsyncd.conf

Then, we need to enter the following data and notice that changes you need to make according to your environment as follows:

uid = swift

gid = swift

log file = /var/log/rsyncd.log

pid file = /var/run/rsyncd.pid

address = 192.168.0.2

[account]

max connections = 2

path = /srv/node/

read only = false

lock file = /var/lock/account.lock

[container]

max connections = 2

path = /srv/node/

read only = false

lock file = /var/lock/container.lock

[object]

max connections = 2

path = /srv/node/

read only = false

lock file = /var/lock/object.lock

Then, we need to edit the following file:

sudo nano /etc/default/rsync

Then we need to search for the line that contains the following data and edit it as follows:

RSYNC_ENABLE=true

Then we have to restart our re-synchronization service as follows:

service rsync start

Then, we need to execute the following command:

sudo mkdir -p /var/swift/recon

chown -R swift:swift /var/swift/recon

This way we have created the directories where the synchronization happens on the destination medium that will save our re-synchronization data.

Now, we finished working with storage services installation and making our basic synchronization services.

## 5.5 Working with Openstack Glance

Glance is our image service that we can use to create virtual machines on our UBUNTU LINUX machine. This is used to create more that one operating system instance running on the same bare-metal hardware, which will permit different architectures and operating system versions to communicate with each other and also will also permit collaboration of different vendors and 3rd party installations to take place and collaborate with each other without the need to use more than one peace of hardware.

First thing that we need to do is:

sudo apt-get install glance

Then, we install the following package to complete the dependencies as follows:

sudo apt-get install python-glanceclient

Now, confirm all the commands by pressing Y and hitting enter key on your keyboard.

We have now installed our glance service and now, let us have to inject our first image that we will download from UBUNTU cloud images directory over the Internet at the following URL as follows:

[https://cloud-images.ubuntu.com/wily/current/](https://cloud-images.ubuntu.com/wily/current/)

This is the last release from UBUNTU LINUX developed by a company called Canonical LTD.

This distribution is one of the most popular cloud images that can be used.

We can now use this image and import it in our Openstack private cloud as follows:

sudo openstack image create --name=”UBUNTU CLOUD IMAGE” --disk-format=qcow2 --container-format=bare --is-public=true < /home/mostafa/Downloads/ubuntu-14.04-server-cloudimg-i386/trusty-server-cloudimg-i386.img --os-username=admin --os-password=AMINPASSWORD --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin

Now that we have completed our Openstack Services installations and configurations.

We have also used some of its services, We also learned how to work with LINUX and learned what are the distributions, repositories, basic commands, and most of the features that LINUX can do.

We also installed basic infrastructure with some advanced features and components from 3rd parties and other vendors.

Thank you so much and appreciate your precious time reading the book.

Hope you enjoy it.