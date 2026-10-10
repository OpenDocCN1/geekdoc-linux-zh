
## Connecting to the Instance

There's a lot of useful information in the **My Instances** list. Of particular interest is the column labeled **Public DNS**, as shown in Figure 5.9.

| Public DNS |
|---|
| ec2-72-44-33-237.compute-1.amazonaws.com |
| ec2-75-101-154-199.compute-1.amazonaws.com |

Figure 5.9. The console showing the Public DNS name of each running instance

Copy the public DNS name for your instance, as you'll need it to connect via SSH.

## Connecting with PuTTY on Windows

Launch PuTTY and paste the Public DNS name into the **Host Name** field, as shown in Figure 5.10.

![](img/4a5ba0dd041e08e6a67fa31d52309995_144_0.png)

Now click the **Auth** tree item (nested inside of the **SSH** item) shown in Figure 5.11 and use the **Browse...** button to locate the private key that you saved from PuTTYgen.

![](img/4a5ba0dd041e08e6a67fa31d52309995_145_0.png)

Figure 5.11. Configuring SSH authentication on PuTTY

Click the **Open** button and **PuTTY** will connect to your instance, authenticating itself using the public portion of your private key. **PuTTY** will then ask you to confirm your request to use the key, as depicted in Figure 5.12.

![](img/4a5ba0dd041e08e6a67fa31d52309995_145_1.png)

Figure 5.12. **PuTTY** confirming use of new key

Click **Yes**, and then enter **root** when your instance prompts you to log in. Since you’ve already identified yourself using your key, a password is unnecessary for the root account. However, if you’ve set up a passphrase for your key you’ll be prompted for it. Figure 5.13 shows a successful login.

![](img/4a5ba0dd041e08e6a67fa31d52309995_146_0.png)

## Connecting with the Mac OS X or Linux Terminal

Open a new terminal window and enter the following command:

```bash
$ ssh -i jeffskeys.pem root@ec2-nnn-nnn-nn-nnn.compute-1.amazonaws.com
```

Replace **jeffskeys.pem** with your own key pair file and *ec2-nnn-nnn-nn-nnn* with the public DNS name of your instance. You’ll receive the following response:

```text
The authenticity of host 'ec2-nnn-nnn-nnn-nnn.compute-1.amazonaws.com (nnn.nnn.nnn.nnn)' can’t be established.
RSA key fingerprint is cd:79:eb:e3:e9:2e:d6:d2:9c:79:65:2a:27:c5:__1b:ba.
Are you sure you want to continue connecting (yes/no)?
```

Of course, the host information and RSA key fingerprint details will be different to those above. If you enter **yes** to the question above, you will be logged in and will receive the following output:

```text
Warning: Permanently added 'ec2-nnn-nnn-nnn-nnn.compute-1.amazonaws.com,nnn.nnn.nnn.nnn' (RSA) to the list of known hosts.
__|__|__|
_| ( __ ) Fedora 8
/ 32-bit
```

```bash
__|__|__|
Welcome to an EC2 Public Image
: -)
     
 Base
 --[ see /etc/ec2/release-notes ]--
[root@domU-12-31-38-00-2E-18 ~]#
```

If you had set a passphrase on your key pair file, you'll be prompted to enter it as well. Again, the host and prompt information will differ to those above.

## Now We're Connected

Congratulations, you now have full control of your very own EC2 instance! If you plan to start up more than one EC2 instance, you should make sure that you can tell them apart by making the shell prompt more distinct. Here's how to set the shell prompt to the string `<dev>:` to indicate that the shell is on a development (as opposed to production) server:

```bash
[root@domU-12-31-38-00-2E-18 ~]# export PS1="<dev>: "
```

Run the following command to see which packages have already been installed:

```bash
<dev>: yum list | grep installed
```

You should see a long list. Feel free to spend some time exploring your new EC2 instance. Try out your favorite Linux commands and verify that they work as you expect them to. You can install new packages using the yum command. If you prefer emacs to vim, install it like this:

```bash
<dev>: yum -y install emacs
```

If you decide to pause at this point, remember that your instance is now running and that you're paying for it by the hour. If there's no need to keep it running, return to the AWS Management Console, select the instance, and choose **Terminate** from the *Instance Actions* menu. When you do this, all data stored on the instance will be lost.

If you launched an EBS-backed AMI, you have an additional option. You can choose **Stop** from the **Instance Actions** menu. The operating system will be cleanly shut down, and the status of the instance will change to *stopped*. Later, you can choose to start the instance again and it will boot up with all the files on the root file system remaining intact. This additional flexibility is among one of the many reasons to prefer EBS-backed AMIs over their older S3-backed cousins.

## Assigning an IP Address

Let’s give this instance a permanent IP address of its own. Close your SSH session with the `exit` command, and then return to the AWS Management Console. Click on **Elastic IPs** in the *Navigation* pane and press the **Allocate New Address** button. Press the **Yes, Allocate** button in the dialog to confirm your wish to allocate a new IP address. After a very brief pause, your newly allocated address will be listed in the **Addresses** list.

At this point the address is yours, but is still unassociated with any particular EC2 instance. Let’s remedy that. Click on the address in the list to select it, and then press the **Associate** button, which will bring up the dialog shown in Figure 5.14.

![](img/4a5ba0dd041e08e6a67fa31d52309995_148_0.png)

Select the appropriate instance ID in the menu, and press the **Associate** button in the dialog. Now create a new SSH session using the Elastic IP address instead of the host name. If you happen to have a spare domain name and a DNS provider, you can map the domain name to the public IP address.

Recall that you’re charged for allocated but unmapped IP addresses. If you decide to terminate your instance and have no need for the IP address anymore, be sure to release it using the AWS Management Console.

## Creating an EBS Volume

Now that you have an instance and an IP address, let's create, attach, and format a storage volume.

Once created, you can attach an EBS volume to any of the instances that are in the same Availability Zone as the volume. Since our instance is already running, let's figure out which zone it's running in. Return to the AWS Management Console, and select the **Instances** view. Click on the row of your instance and inspect the detailed instance properties displayed at the bottom, as shown in Figure 5.15.

![](img/4a5ba0dd041e08e6a67fa31d52309995_149_0.png)

My instance is in zone `us-east-1a`. Click on **Volumes** in the **Navigation** pane, press the **Create Volume** button, and you will be presented with the dialog box shown in Figure 5.16.

![](img/4a5ba0dd041e08e6a67fa31d52309995_149_1.png)

The dialog form accepts values in units of **gibibytes** (GiB) and **Tebibytes** (TiB). These are the power-of-two analogs of the more familiar gigabytes (GB) and terabytes (TB), both of which represent powers of ten. One gibibyte is 1,073,741,824 bytes, whereas one gigabyte is 1,000,000,000 bytes.

Enter the desired volume size (10GiB is a good value) and select the Availability Zone of your instance. Leave the other fields as they are and press the **Create** button. The new volume will appear in the EBS Volumes list, with a **creating** status. Wait a few seconds, press the **Refresh** button, and the status should change to **available**.

Now select the volume and press the **Attach** button (or right-click on it and choose **Attach Volume**) to reveal the Attach Volume dialog shown in Figure 5.17.

![](img/4a5ba0dd041e08e6a67fa31d52309995_150_0.png)

Figure 5.17. Attaching an EBS Volume to an Amazon EC2 instance

Select your instance, keep a record of the value in the **Device** field, and press the **Attach** button. Refresh the EBS Volumes list until the **Attachment Information** column contains the word “attached.”

At this point the new EBS volume is attached to your instance, but not yet ready to store files. Head over to your SSH session and put a file system on the newly attached volume:

```bash
<dev>: mkfs -F /dev/sdf
```

After this command completes, `/dev/sdf` is ready to store files. Create a mount point and mount the file system on it like this:
