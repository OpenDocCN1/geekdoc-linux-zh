
partitions on the system from a rescue disc. That way you can then perform forensic analysis on the image without overwriting the original evidence. Plus, once you have an image to work from, you can consider redeploying the server. If the host is a VM and you were able to take a snapshot, you have even more data to work from. Create a copy of the entire VM, snapshot and all. Then you can potentially replay the time you discovered the attack over and over and run tools on the running snapshot image without fear of corrupting data. If you have the space, consider creating two images. One is a gold image that you put away and don’t touch, and the other is an image that you use for any forensic analysis you might perform. When you have multiple images, if you make a mistake and accidentally write to one during your analysis, you will at least have the gold image to copy from.

## Server Redeployment

Another thing to consider before a crisis occurs is whether and when you should rebuild a server. The best practice is to rebuild a server whenever there has been a breach. It can be easy, at least if the attacker was sloppy, to prove he or she did install a root kit if you see the software out in the open, but unless you are skilled at forensic analysis it can be difficult to prove an attacker didn’t install a root kit or some sort of Trojan horse on the system. A root kit can hide all sorts of things from the administrator, so unless you are absolutely sure there is no root kit, rebuild the machine.

How you go about rebuilding the server might be decided on a case-by-case basis. Some servers (particularly those in a cluster) often can be rebuilt from scratch without a thought. Other servers, such as large database or e-mail servers that aren’t in a cluster, can be more difficult because they hold data you need to transfer to the new host. These types of machines might have to go into quarantine until you can make sure that the data can be trusted. To be safe, you might even have to try to track down when the attack occurred and roll back the files on the system from a previous backup. Also, you might need to keep the machine in quarantine until you can track down how the attacker got in and patch the hole before risking another intrusion.

## Forensics

Once you have a valid image of the system's partitions, you might want to perform some sort of forensic analysis on it. Computer forensics is a vast topic and it can take years of work for you to become proficient. That having been said, even if you aren't a skilled forensics expert, you might want to try your hand at identifying how the attacker got in.

One basic method of forensic analysis is simply to take the image of your attacked server to another host, mount it loopback and read-only, and then look around the mounted system for clues. For instance, if I had an image of a partition on an external USB drive mounted at /media/disk1/ and the image itself was at /media/disk1/web1-sda1.img, I could use the following command to mount the disk at /mnt/temp:

```
$ sudo mkdir /mnt/temp
$ sudo mount -o loop,ro /media/disk1/web1-sda1.img /mnt/temp
```

If you are ready for more advanced forensic analysis, I recommend you check out Sleuth Kit (http://sleuthkit.org). Sleuth Kit is a complete set of forensics tools including a Web-based front end called Autopsy. These tools are packaged in Ubuntu as sleuthkit and autopsy, so you can install them on an Ubuntu desktop with your preferred package manager. Once both tools are installed, type autopsy in a terminal to start the program and then follow the instructions on the screen to see where Autopsy stores its files (/var/lib/autopsy by default) and what URL to open on a Web browser to use Autopsy (http://localhost:9999/autopsy by default). That URL will display the default Autopsy page as shown in Figure 6-1, and from there you can navigate through the tool, start a new investigation, and add images to scan. For more information on how to use Autopsy, read the official Autopsy user's guide at http://wiki.sleuthkit.org/index.php?title=Autopsy_User's_Guide.

Another useful forensics tool is chkrootkit. This program can check a file system for common root kits and then output a report. This tool is also packaged for Ubuntu with the package name chkrootkit. Note that you generally don't want to run this on a live system because you will potentially overwrite evidence. Instead, mount an image somewhere on your
