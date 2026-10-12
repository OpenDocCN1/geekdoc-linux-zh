# Get alerts with the Raspberry Pi baby monitor

# Projects

![](bbox=[0.02, 0.08, 0.99, 0.41])

```
`tail -f /var/log/syslog`
and
```
dmesg | tail
```
```

This will display any issues that the process is currently having, which is intended to (and hopefully will!) help you diagnose and resolve any problems.

Most issues will be driver-related, so keep this in mind with USB webcams. Press CTRL+Z to end

![](bbox=[0.03, 0.45, 0.27, 0.61])

# Check saved images

+   14. To confirm the quality of the images captured by the Raspberry Pi baby monitor, boot into the GUI (or install tightv server and remote connect) and browse to /var/lib/motion to see how they are turning out. This should give you the info you need to adjust the dimensions of the captured images.

# Troubleshoot camera connectivity

+   15. There’s no guarantee that motion will work straight away. If no images are found, or you can’t connect to the stream, run:

# Name your images

+   16. Images collected by the motion software can be configured with a specific naming convention, based on date and time.
+   
+   You can find these listed under target_base_directory in motion.conf. For instance, you can specify a folder for new images, based on date:

```
`target_base_directory ~/pic%Y%m%d%H%M%S-%t`
Note the “%” — both directory and
```

images will be named according to date, with images also labelled with the timestamp

# Go beyond your home network

+   17. Wouldn’t it be great to monitor your child’s sleep from your favourite restaurant? You can do this by installing the No-IP software on your Raspberry Pi.
+   
+   This software enables you to get around the fact that your ISP won’t give you a dedicated IP address without paying a hefty premium, by installing a client app that enables you to view the baby monitor outside your home network.
+   
+   Head to www.noip.com and check their knowledge base for details