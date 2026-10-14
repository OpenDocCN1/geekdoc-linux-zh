pre- or post-install script that parses /proc/cmdline and stores those settings into environment variables. Then you can refer to those environment variables in your script and make custom changes to the pre- or post-install process based on them.

For instance, let’s say we want to define two cheat codes at the boot prompt: mytype, to label what type of server it is (Web, MySQL, DNS), and myraid, which tells whether it should use RAID or not. Instead of setting up three different Kickstart files, I could use a single Kickstart file that then has logic in its pre-installation script to parse these options and change settings based on them. Here’s a sample pre-install script that would parse the /proc/cmdline file, set the environment variables, and then perform special actions based on them:

```
%pre
for i in `cat /proc/cmdline` ; do
echo $i | grep -iq MYTYPE=
if [ $? -eq 0 ] ; then
export MYTYPE=`echo $i | awk -F"=" '{ print $2; }'`
fi
echo $i | grep -iq MYRAID=
if [ $? -eq 0 ] ; then
export MYRAID=`echo $i | awk -F"=" '{ print $2; }'`
fi
done

if [ $MYTYPE == "web" ]; then
# Change preseed settings for web servers
elif [ $MYTYPE == "mysql" ]; then
# Change preseed settings for mysql servers
elif [ $MYTYPE == "dns" ]; then
# Change preseed settings for dns servers
fi

if [ $MYRAID ]; then
# Change preseed settings for RAID
fi
```

Now at the boot prompt if I wanted to set up a MySQL server with RAID, I could type install1 mytype=mysql myraid=1. Again, the advantage to this approach is that it allows you to maintain a single Kickstart file that has the logic within it to change settings for specific server types. The downside to