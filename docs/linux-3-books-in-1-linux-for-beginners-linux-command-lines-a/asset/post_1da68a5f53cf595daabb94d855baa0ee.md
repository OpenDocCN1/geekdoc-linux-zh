
## drive form the BIOS settings in your system

It is important to understand that each system has its own user interface for the BIOS settings depending on the manufacturer. Therefore, you need to select the boot priority settings carefully. Once you do this, you need to reboot the system and the first thing on your screen will be the Kali Linux boot menu. You can choose the Live option that is the first option when it comes to booting Linux from the USB drive directly.

## Linux Persistent Installation

It is important to remember that the size of the memory you have matters, especially if you use a USB drive to install Kali Linux on your system. Depending on the type of operating system you use, you need to create a Kali Linux USB drive. You need to ensure that the GParted application is installed on your device before you work on installing Kali Linux. If you have trouble with installed GParted, you need to read the documentation and see what you should do to get rid of any errors during installation. You can use any of the following commands in the terminal to install this tool:

```
apt-get install gparted
aptitude install gparted
yum install gparted
```

Once you have GParted downloaded on your system, you need to download the Kali Linux ISO from the official website and plug the USB drive onto your computer system. You need to use the command below in the Linux terminal if you want to see where the USB drive is present.

```
mount | grep -i udisks | awk '{print $1}'
```

The file in the USB drive will be saved using the name /dev/sdb1. You must ensure you look at the right file when you install Linux on your system since the file can be different from one system to the next. In the following command, you can remove the numbers at the end to ensure you switch between file names.

Use the dd command to write the Kali Linux ISO to the USB drive as follows.

```
dd if=kali_linux_image.iso of=/dev/sdb bs=12k
```

Launch Gparted application using the following command.

```
gparted /dev/sdb
```

You should now have one partition in your drive which has the Kali Linux image on it. The next thing to do is create another partition in the drive by right-clicking on the drive and selecting the ‘New’ option from the menu. This will appear once you select the partition menu available in the Menu bar. The following are the steps you need to follow, and they may vary depending on the machine you use:

- The unallocated space in the drive is greyed out
- You should now select the new option from the partition using the drop-down menu
- You can specify the size of the drive using a graphical slider
- Now, choose the file system and update it to ext4
- Select the add option and click on the drop-down menu. You need to select the option to apply all the operations on your system
- When you see a prompt, click ok, and the settings will update

You can add a persistence function to the USB drive using the following commands.

```
mkdir /mnt/usb
mount /dev/sdb2 /mnt/usb
echo "/ union" > /mnt/usb/persistence.conf
umount /mnt/usb
```

That is it. You have now created a persistent Live Kali Linux USB. Reboot your system and you should be able to boot the Kali Linux operating system from the USB drive.

# Chapter Eleven

## The Penetration Testing Life Cycle

As a system administrator, you need to perform penetration testing in your organization to ensure you have the right security enabled in your network and server. In this chapter, we will look at the different stages used in penetration testing. Using this chapter, you will learn more about system administrators' different tools and the processes they need to follow during each stage. This way, you will understand the five stages of the penetration testing lifecycle and have an idea of the tools used by security professionals while engaging in penetration testing.

### The Five Stages of the Penetration Testing Life Cycle

In this section, we will look at the five stages in the penetration testing lifestyle, and the information is broken down easily to help you understand what exactly is expected out of you during each stage.

#### Stage 1: Reconnaissance

This is the first step in the penetration testing phase. Let us assume you are running a military operation. The officers and analysts are going through the foreign territory map, and others in a different room are looking at the news and trying to see what can be done to take down the enemy. Another group is working on the information they need to collect to ensure the team can move into the enemy territory and make it their own. You need to do this when you work on a penetration test during your ethical hacking process.

If you do not have the expertise to run a penetration test, the organization will hire a team to perform this test. During this phase, you need to discover the information about the target system and also gather information about the system using public and private sources. You can do this easily by looking for information about the Internet since most information is publicly available. During this stage, you need only to understand what is present in the target's network and server. You do not breach the network and server since you only have to scan and document the information you will need while performing the next few steps.

#### Stage 2: Scanning

Let us consider that you are on a military mission with a team of people, and there is a hilltop you need to reach. This hilltop is behind your enemy lines, and one of your soldiers is hidden in the bushes. This soldier will come back and give you information about the enemy camp. The objective of this mission is for you to determine the type of activities the enemy is performing. This soldier will also tell you about the different ways you can move into enemy land and the security that is around the camp.

This soldier was told what he needed to do for him to get the information he needed. He was told what he had to look at. This is exactly what you do in the reconnaissance stage. You gather information, and it is this information you use during the scanning stage to determine which server and network you need to scan to find any vulnerabilities. You can use various tools to scan the target network, and Kali Linux comes with in-built options. You need to use the information you collect during this stage during the exploitation phase to determine which areas you need to exploit so that you can extract information.

#### Stage 3: Exploitation

If you are performing the penetration testing with a team, you need to ensure you move through the network and server easily without being detected. You also need to find a way to enter the server without getting caught. You need to find the right gaps in the server and enter the system and network through the server's open door. You also need to spend time inside the server and see what information you can extract from the system. You need to do this during the exploitation stage. The objective is to ensure you quickly enter and exit the network and server with the information you need without being detected by anybody. During this stage, you need to exploit the system and find sensitive information about the business. You can do this repeatedly if you need to.

#### Stage 4: Maintaining Access

When you perform the penetration test, you must ensure you have unlimited access to the servers and network you are using. You need to ensure there is access to all the information you need. As the system administrator, you need to find a way to keep access while you discover how to enter the target system and network. You also need to find a way to exploit the server and see what information you can obtain or access through the network. You also need to find a way to get in and out of the system without getting caught. Therefore, with the information gathered in the exploitation state, they automate a way to keep their access continued to the target system.

#### Stage 5: Reporting

When you perform penetration testing on your system and server, you need to stand in front of the entire team and the higher-ups to tell them what you learned from the penetration test you performed. You need to explain every step and detail everything you found during the test. You need to expand the details of your findings. At the end of the penetration testing lifecycle, you also need to prepare a report which explains each phase of your penetration test. You need to explain the loopholes discovered, the vulnerabilities exploited and the servers, networks and systems targeted during the test. In some cases, you may need to provide information about the findings. You need to ensure management will look at the different means they can use to protect their servers and networks.
