# LFS From Scratch - Version 9.0

LFS assumes that the root file system (/) is type ext4. To create an ext4 file system on the LFS partition, run the

```
mkfs -v -t ext4 /dev/<xxx>
```

If you are using an extra swap partition, there is no need to format it. If a new swap partition was created, it will need to be initialized with this command:

```
mkswap /dev/<yyy>
```

Replace <yyy> with the name of the swap partition.

# 2.6. Setting The $LFS Variable

Throughout this book, the environment variable LFS will be used several times. You should ensure that this variable is always defined throughout the LFS build process. It should be set to the name of the directory where you will be building your LFS system - we will use /mnt/lfs as an example, the directory choice is up to you. If you are building LFS on a separate partition, this directory will be the mount point for the partition. Choose a directory location and set the variable with the following command:

```
export LFS=/mnt/lfs
```

Having this set is beneficial in commands such as mkdir -v $LFS/tools can be typed literally. The shell will automatically replace "$LFS" with "mnt/lfs" (or whatever the variable was set to) when it processes the command line.

> Caution
Do not forget to check that $LFS is set whenever you leave and reenter the current working environment (such as doing a su to root or another user). Check that the LFS variable is set properly with:

echo $LFS
Make sure the output shows the path to your LFS system's build location, which is /mnt/lfs if the provided example was followed. If the output is incorrect, use the command earlier on this page to set $LFS to the correct directory.

One way to ensure that the $LFS variable is always set is to edit the .bash_profile in both your personal home directory and in /root/.bash_profile and ensure the export command above. In addition, the shell in /etc/passwd file for all users who need the LFS variable needs to be bash to ensure that the /root/.bash_profile is incorporated as part of the login process.

Another consideration is the method used to log into the host system. If logging in a graphical display manager, the user's .bash_profile is not normally used when a virtual terminal is started. In this case, add the export command to .bashrc for the root. In addition, some distributions have instructions to run the .bashrc instructions in a non-interactive bash invocation. Be sure to add the export command before the test for non-interactive use.

17