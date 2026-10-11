by root. The default behavior of ssh-keygen when executed by root, however, is to generate User Keys for root. So, in order to generate new Host Keys, simply use the -o option as shown in Example 11-25. Make sure that you do not specify a passphrase for Private Host Key! When ssh-keygen prompts you for a passphrase, press return.

# **Example 11-25 Generating New Host Keys**

```
roadrunner$ ssh-keygen -f /etc/ssh/ssh_host_key
Initializing random number generator...
Generating p: ****(distance 116)
Generating q: .............................++* (distance 386)
Computing the keys...
Testing the keys...
Key generation complete.
/etc/ssh/ssh_host_key already exists.
Overwrite (y/n)? y
Enter passphrase: <carriage return>
Enter the same passphrase again: <carriage return>
Your identification has been saved in /etc/ssh/ssh_host_key.
Your public key is:
1024A431E6914F72264014628092156127882547631863043012215095713
55676043599904415535717946608285625971378289394141213273076838
876521925431369047609136164173710423934872200497352070242221
81830754515873790764004515033791928990763072756634927773098538
955985906935296575657355575292968238763934404313208076927
5239853307 root@roadrunner
Your public key has been saved in /etc/ssh/ssh_host_key.pub
roadrunner$
```

Once you have generated new Host Keys, don't forget to remove the old Public Host Key entries from the `/etc/ssh/ssh_known_hosts` and `~/.ssh/known_hosts` files throughout your computing environment. Otherwise you will get the error message as displayed in Example 11-9 on page 287 and be unable to use X Window System and agent forwarding capabilities.

> **WARNING!**
> 
> You must not specify a passphrase for the Private Host Key! If you do, the system will not be able to utilize its Private Host Key, which is necessary for the initial RSA Host-Based Authentication. One way to avoid supplying a passphrase for the Private Host Key is to use the command
> # ssh-keygen -f /etc/ssh/ssh_host_key -N ""
> You may then alias this command to something like host-keygen. This should help avoid mistakes.
> On the other hand, you should utilize a passphrase for root's Private User Key.

**Disabling Direct root Access.** We noted in Table 11.5 on page 270 that root access via ssh can be disabled by setting the PermiRootLogin option in `/etc/ssh/sshd_config` to no. The benefit of this approach is that no one, especially the bad-guys, will be able to connect to root via SSH. If you eliminate root access in this way, you will need to permit su (see Access Control with