```
```bash
__|\__|__|  
Welcome to an EC2 Public Image
: -)  
     
 Base  
 --[ see /etc/ec2/release-notes ]--  
[root@domU-12-31-38-00-2E-18 ~]# 
```
```

If you had set a passphrase on your key pair file, you'll be prompted to enter it as well. Again, the host and prompt information will differ to those above.

# Now We're Connected

Congratulatlons, you now have full control of your very own EC2 instance! If you plan to start up more than one EC2 instance, you should make sure that you can tell them apart by making the shell prompt more distinct. Here's how to set the shell prompt to the string `<dev>:` to indicate that the shell is on a development (as opposed to production) server:

```
```bash
[root@domU-12-31-38-00-2E-18 ~]# export PS1="<dev>: "
```
```

Run the following command to see which packages have already been installed:

```
```bash
<dev>: yum list | grep installed
```
```

You should see a long list. Feel free to spend some time exploring your new EC2 instance. Try out your favorite Linux commands and verify that they work as you expect them to. You can install new packages using the yum command. If you prefer emacs to vim, install it like this:

```
```bash
<dev>: yum -y install emacs
```
```

If you decide to pause at this point, remember that your instance is now running and that you're paying for it by the hour. If there's no need to keep it running, return to the AWS Management Console, select the instance, and choose **Terminate** from the *Instance Actions* menu. When you do this, all data stored on the instance will be lost.