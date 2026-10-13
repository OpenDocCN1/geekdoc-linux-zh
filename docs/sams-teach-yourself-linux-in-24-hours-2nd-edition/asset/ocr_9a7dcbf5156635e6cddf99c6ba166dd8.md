# Q&A

Q I screwed up my LILO installation! My system won't boot to OpenLinux!

A This is probably an error in the /etc/lilo.conf file. Use the OpenLinux boot diskette to reboot your computer. At the command line, type linux root=/dev/your_hard_drive (such as /dev/hda1). See the BootPrompt-HOWTO under the /usr/doc/HOWTO directory.

Q What are some good documents to read about installing OpenLinux?

A Although you can find many different documents installed under the /usr/doc/HOWTO or /usr/doc/HOWTO/mini directories, such as Linux+Win95, Loadlin+Win95, or the Linux Installation Guide, you should first read the technical documents, FAQs, and errata at http://support.calderasystems.com/caldera or http://www.calderasystems.com/support/techguide.html.

# Exercises

+   1. Try rebooting your computer. Press the Tab key at the LILO boot prompt. What happens?
+   2. At the LILO boot prompt, type vga=ask, and press Enter. What happens?
+   3. After pressing Enter in the previous exercise and starting the boot process to OpenLinux, what happens next?

![](bbox=[0.88, 0.28, 0.99, 0.45])