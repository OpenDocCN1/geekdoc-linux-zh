
```bash
local myarray
myarray=(`echo "$@"`)
echo "This the new value of the array: ${myarray[*]}"
```

thisarray=(1 2 3 4 5 6 7 8 9 10)
echo "This the original value of the array ${thisarray[*]}"
testingfunction ${thisarray[*]}
```bash -f main.sh```

This the original value of the array 1 2 3 4 5 6 7 8 9 10

This the new value of the array: 1 2 3 4 5 6 7 8 9 10

The variable named $thisarray contains the individual array values, placing them on the function’s command line. The function then builds the array variable using command line parameters and, once you are in the function, you can use the array as you would any other array.

```bash
$ cat test11
#!/bin/bash
function addingthearray {
    local sum=0
    local thisarray
    thisarray=(`echo "$@"`)
    for values in ${thisarray[*]}
    do
    sum=$[ $sum + $values ]
    done
    echo $sum
}

iarray=(1 2 3 4 5 6 7 8 9 10 11 12 13)
echo "This is the original value of the array: ${iarray[*]}"
arg1=`echo ${iarray[*]}`
therealresult="addingthearray $arg1"
echo "This is the final result : $therealresult"
bash -f main.sh
```

This is the original value of the array: 1 2 3 4 5 6 7 8 9 10 11 12 13

This is the final result: 91

## Handling User Input

You have learned how to write shell scripts that interact with data, files, and variables on a Linux operating system. However, sometimes you need to write a script that must interact with a person who is running the script. The shell gives us several methods to retrieve data from people, including some command line parameters, command-line options, and reading input from the keyboard. The chapter will walk you through the process of incorporating different methods in the bash shell scripts to get data from the person who is running the script.

Variables called positional parameters are assigned to the command line parameters by the bash shell, including the name of the program executed by the shell. We use standard numbers for the positional parameter variables - $0 is the program name, $1 is the first parameter, $2 the second one, and so on up to $9.

## Conclusion

Now that you have reached the end of the book, you should have a good grasp of Linux command line and shell scripting. Unlike other operating systems, the Linux operating system is complicated. You don’t get to see a graphical interface where you can work with a mouse. It is the “all-keyboard” thing that makes Linux hard to learn. However, it is not that hard with this book in your pocket. You can use this book as a reference guide whenever you operate the Linux command line or jump to the editor to write shell scripts. Being consistent and regularly practicing with codes will help you learn the commands and codes faster than just reading the scripts.

Keep this book by your side and you’ll always have keyboard shortcuts and commands at your fingertips. Now, let’s get started with Linux!

## References

- 22 best Linux text editors for coding (2020 Reviews). (2020, July 12). Knowledge Base by phoenixNAP. https://phoenixnap.com/kb/best-linux-text-editors-for-coding
- Bash while loop examples. (2020, November 5). nixCraft. https://www.cyberciti.biz/faq/bash-while-loop/
- Blum, R. (n.d.). Linux Command Line and Shell Scripting. https://inf.ocs.ku.ac.th/Download/Wiley_Linux_Command_Line_and_Sh
- Broida, R. (2017, February 9). How to install Linux. CNET. https://www.cnet.com/how-to/how-to-install-linux/
- Ward, B. (n.d.). How Linux Works. index-of.es/. https://index-of.es/Varios-2/How%20Linux%20Works%20What%20Every%20Superuser%20Sh

# LINUX SECURITY AND ADMINISTRATION

Andy Vickler

## Introduction

![](img/aae83b54a1b1783f3f5369bd9062b27c_264_0.png)

If you are new to using Linux, it will be difficult for you to find the right information online. This book has all the information you need to help you install the operating system and show you how you can use it either on your system or a virtual system. The book also has information about how you need to configure user access and other information to maintain the network and server's security on the Linux system. You do not have to know anything about Linux before you use it since the information in this book will guide you every step of the way!

The book introduces the idea of using Linux on a virtual system and provides information on the different distributions of Linux. You can use this information to determine which distros work best for you and download that onto your system. You will also learn about the importance of a root account and the other accounts on the server. The book also provides information about the methods used to control access to users. You will learn how you can grant and revoke privileges to users to help you protect the data.

The book covers how you can secure the information, files, and folders in the operating system. You will be introduced to a list of tools you can use to secure the data on your systems and how you can encrypt and decrypt information using these tools. You can also use passwords to encrypt and decrypt the files and folders on the server and network if you need to.

Since Linux is an operating system, and the data is stored on a server or network, you need to test the network and server's strength. This book will shed light on the method you can use to identify any vulnerability in the system. It will also let you know how you can use scanning to identify the holes in your system. You can use the information in this book to determine how to overcome those vulnerabilities.

Thank you for purchasing the book. I hope you learn more about Linux and how you can protect the information in your files and folders.

## Chapter One: Using Linux on Virtual Machines

Have you wanted to use Linux but did not want to use it on your system? Your system may have trouble if you use dual-booting, and the best thing to do is to use Linux on a virtual machine. It is easy for you to use Linux on a virtual machine if you use Windows. The procedure is straightforward. In this chapter, we will look at installing and using Linux on a virtual machine, a VMware Workstation specifically.

If you want to use a virtual machine, you need to find a PC, which allows you to use virtualization. You may have tried to install Linux on your system using a CD, but you may not be sure about dual booting. You should install the Linux operating system on your PC but using a virtual machine.

Virtual machines are environments that replicate the conditions of the hardware on your device. The environment mirrors everything in your personal computer and is limited only by the system's different components. This means you cannot expect to have a four-core CPU on a processor which only has two cores. You can achieve virtualization on multiple systems, and the result of this will be superior on computers that have CPUs that support visualization.

You can use different virtual machines to install the Linux operating system on your computer. VMware is one of the leading manufacturers of virtual machines and applications. In this chapter, we will look at how you can install Linux OS in Windows using a workstation player designed by VMware.

### Installing a Workstation Player

If you want the workstation player, you need to download the latest version from the VMware website. They constantly upgrade their workstation player application and tool. For this example, we will use the VMware workstation 15 player, and this file is 150 MB in size. The latest versions can be heavier, so make sure you have good Internet connectivity.

These workstation players are available for home, non-commercial, and personal use and are free. Non-profit organizations and students can use this version since they do not have to shell out any money on installing the operating system. A VMware workstation player performs all the functions a standard virtual machine must. You can also use VMware products since each product offers a wide range of visualization solutions that you can use for any business. If you want to learn more about their products, you can read about them on their website. After you download the VMware workstation player, click on the installer and follow the installation wizard steps to set up your virtual workstation. It is recommended that you download the Enhanced Keyboard Driver during the installation since you may not need it now but will need it later. Complete the installation and reboot your system when the wizard prompts you.

### Choose the Correct Distro

You should read about the different Linux distributions available to you and choose the one that works best for you. Some Linux distributions work best on virtual machines, while others cannot work on them. All 64-bit and 32-bit versions of Linux work well on virtual machines. You cannot run Linux distros, such as Raspberry Pi and other ARM architecture Linux distributions on virtual machines. If you want to use an ARM Linux environment on your Windows machine, you should try QEMU. If you do not know which distro you need to choose, choose any from the list below:

### Linux Distros

Since there are many options available, you may find it hard to choose the right Linux distro for your system. How do you know that is the best one you should use for your system? What if you want to game using Linux distros? Do you want to use a pretty distro that uses the same structure as macOS?

In this section, we will look at the different Linux distros lists available for you. These distros have been used actively by various individuals over the last few years. It is best to download a Linux distro that you can use safely on your system. You should also check if the distro you use is updated regularly using security patches.
