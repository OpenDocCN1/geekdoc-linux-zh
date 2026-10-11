
99536578
44768915
90480600
82281337
56945099

Do you want me to update your `/root/.google_authenticator` file (y/n) y

Do you want to disallow multiple uses of the same authentication token? This restricts you to one login about every 30s, but it increases your chances to notice or even prevent man-in-the-middle attacks (y/n) y

By default, tokens are good for 30 seconds and in order to compensate for possible time-skew between the client and the server, we allow an extra token before and after the current time. If you experience problems with poor time synchronization, you can increase the window from its default size of 1:30min to about 4min. Do you want to do so (y/n) y

If the computer that you are logging into isn't hardened against brute-force login attempts, you can enable rate-limiting for the authentication module. By default, this limits attackers to no more than 3 login attempts every 30s. Do you want to enable rate-limiting (y/n) y

### Step Three

You should now edit the configuration file for your SSH port. The file is called `vim /etc/ssh/sshd_config` and you can access it using PAM (pluggable authentication module). You need to run the following command before you save the changes and close the file:

```
UsePAM yes
ChallengeResponseAuthentication yes
```

Now, you can restart the server using the command below:

```
systemctl restart ssh
```

### Step Four

Now that you have the SSH set up, you need to edit another configuration file where the PAM is present. This file is for the SSH daemon. You need to add the following command to the file `vim /etc/pam.d/sshd`: `auth required pam_google_authenticator.so`.

### Step Five

You now have to save the file down. Close the file and reboot the server. You will now be authenticated using Google authenticator.

## Turning Off Internet Protocols

It is important to identify which Internet protocol (IPv4 or IPv6) you use frequently. For instance, if you do not use the IPv6 protocol frequently, you need to disable it in the configuration file. Add the following lines of code to the configuration file to do this:

```
vim /etc/sysconfig/network
NETWORKING_IPV6=no
IPV6INIT=no
```

## Understanding the Applications/Tools before Installation

Before you install an application or tool on your server, you need to see if any new software or tools are being added to the server along with the application. This will put your server at risk since it will add a newer opening to the server, leading to a vulnerability.

## Removing Unnecessary Startup Processes

Linux has various startup processes which run in the system, and these are called targets. You need to look at the settings and see what you need to change or update before you make the change in the configuration file. You can set up servers to ensure they have only the required packages or servers set. This will reduce the amount of time you spend cleaning up your server space.

## Reviewing Activities Regularly

Every file on Linux will be located on the server and the infrastructure. You can access the folder or directory with the backup. In this directory, you will have details of all the files on the server and the different logs and their details. You need to review the logs regularly to ensure no unauthorized activities are being performed on the server. If you want to look at the file, you can run the command: `less file.log`. You can use different commands to go through the logs in the directory.

## Start Backing Up

In case of any disaster to the server or a hack, it is important for you to have a backup. A backup is your last line of defense, and it is recommended you follow the backup method 3 − 2 − 1. In this method, you need to do the following:

- **Step One**: Maintain 3 copies of your data – one will be the primary source while the other two will be the backups
- **Step Two**: You need to store the data on at least two storage media, such as tape drives, cloud, local drives, etc.
- **Step Three**: There needs to be one copy of the data stored offsite

It is also important for organizations to account for these backups and ensure they have details of any failed backups. Linux is a mature system, and it is quite secure when compared to other operating systems. The operating system has an unparalleled ability to adapt to and set up different configurations. Therefore, it is one of the best systems to use if you want to have a self-managed and secure system. Linux also offers you to use a dedicated server option, and this is stable and fast.

## Only Install the Things You Need

This is an important thing to bear in mind – do not download everything you find. You need to install the packages you want to use. Your server should never be overloaded. This means you should only install those packages, applications, and tools on your server if you need them. If you find any application, server, or package on your system that is not required, you need to remove it. If you have fewer packages on your server, you can avoid patching the code.

## Use SELinux

SELinux is an enhancement you need to make to the kernel, and this uses a MAC or Mandatory Access Control system to ensure any application or tool is defined based on a set of resources. If you want to install the package, use the following command: `apt-get install selinux-basics selinux-policy-default auditd`.

Once you download the package, you need to load the policy script. This is a modified version of the actual script and is included as part of the SELinux package. You should then move this script to the folder, `/usr/share/initramfs-tools/scripts/init-bottom/`, and run the command written below: `update-initramfs -u`. You can use this to update the SELinux package. Once you do this, you need to run the following command to configure PAM, GRUB, and auto relabel creations: `selinux-activate`.

You should now reboot the server and ensure the changes that you have made have taken effect on your server. It may take your system time for you to label the file systems when you boot the server. The system will reboot for the second time when it has labeled the files accurately. Now, run the command and ensure you have everything set up accurately on your server and system. Performing an audit by yourself will help you find different problems in the installation of SELinux. You can learn more about this using the Debian SELinux documents.

SELinux or Security-Enhanced Linux is a security mechanism provided by Linux developers which can be used in the kernel. SELinux provides three operations:

- **Disabled:** When you use this mode, you can disable the use of SELinux on your server
- **Permissive:** If you use this mode, you will only receive a warning or alert when unauthorized activity is performed on the server. It will also log the actions performed by the user
- **Enforcing:** In this mode, the functions of SELinux are not limited, which means it looks at every aspect of the security of your server

You can manage the modes using the `/etc/selinux/config` file.

## Securing the Console Access

It is important to protect a Linux server from end-to-end, which means you need to protect the server's access through a console. You need to disable the use of external devices, such as USB pens, CDs, or DVDs, once you set up the BIOS. You also need to set up the BIOS and use the grub boot loader password to protect the updated settings.

## Restricting the Use of Old Passwords

You can ensure users do not use old passwords when they are prompted to update their passwords. Your Linux server will save the old passwords in the file /etc/security/opasswd. You can ensure your server does this using the PAM module. If you are unsure of how to do this, follow the steps given below:

- If you use CentOS, Fedora or RHEL, you can open the file `/etc/pam.d/system-auth`. To do this, run the command: `# vi /etc/pam.d/system-auth`
- If you use Ubuntu or Debian, you can open the file `/etc/pam.d/common-password` using the command `# vi /etc/pam.d/common-password`
- You need to add the following command to the auth section in your configuration file: `auth sufficient pam_unix.so likeauth nullok`

Once you do this, you need to add the following lines to the configuration file to ensure a user does not reuse his last few passwords. You can decide the number of passwords you want the server to store.

```
password    sufficient    pam_unix.so nullok use_authtok md5 shadow remember=5
```

This line will indicate to the server that it needs to remember the user's last five passwords. So, if the user enters one of the earlier passwords, he will receive an error from Linux asking him to choose a different password.

## Checking Listening Ports

You need to look at the different ports in your server and view them along with the services they provide. To do this, you can run the following command: `netstat -tunlp`. Based on the list you receive, you can determine if there are any ports you need to disable from the system. You can do this using the command `chkconfig`. You can then close all the ports in the server which you do not need. To do this, you can run the command: `chkconfig`
