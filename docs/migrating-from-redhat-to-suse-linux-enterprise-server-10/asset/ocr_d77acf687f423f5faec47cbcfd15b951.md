# Figure C-9

Step 4
| | Boot and Start the Installation |
| :--- | :--- |
| | Red Hat Enterprise Linux | SUSE Linux Enterprise Server |
| | 1. Boot with CD # 1 | 1. Boot with CD # 1, and when the CD menu shows, choose the *Installation* option |
| | If the *ks.cfg* file is on a floppy, enter the following at the boot prompt: | 2. Press *F3* and choose the appropriate installation source, then fill in the server IP address and directory text boxes |
| | *linux ks=floppy* | |
| | 2. Booting with the customized CD | *Note:* Alternatively, you can enter |
| | If the *ks.cfg* file is on the customized Boot CD, enter the following at the boot prompt: | *install=proto://server/dlr where* *proto* is the NFS\|HTTP\|FTP protocol, *server* is the IP address of the server and *dlr* is the directory where the packages reside |
| | *linux ks=cdrom:/ks.cfg* | |
| | 3. For NFS installation, enter the following at the boot prompt: | 3. Press *F5* and choose the *Verbose* option to show all messages during the installation for troubleshooting purposes |
| | *ks=nfs:server:/dlr/ks.cfg* | |
| | 4. For HTTP installation, enter the following at the boot prompt: | 4. In the *GRUB* *Boot* *Options* text box, enter one of the following: |
| | *ks=http://server/dlr/ks.cfg* | - For NFS installation: |
| | 5. Once you press *Enter*, the installation should begin and finish without any need for interaction | *autoinst=nfs://server/dlr/autoinst.xml* |
| | | - For HTTP installation: |
| | | *autoinst=http://server/dlr/autoinst.xml* |
| | | - For disk-based installation: |
| | | *autoinst=device:/fsid1/autoinst.xml* |
| | | 6. Press *Enter* to execute the installation; no further interaction should be necessary |

![](bbox=[0.84, 0.14, 0.88, 0.17])

# Install Modes

Not only do Red Hat Enterprise Linux and SUSE Linux Enterprise Server provide the ability to use different types of installation media for the source of the installation, but they also provide several different install modes (ways to perform the installation).

Typically, Linux installations are performed directly via the locally attached keyboard monitor and mouse. However, in some cases (such as on mainframes or headless servers), this may be impossible. Instead of relying on expensive third-party components such as IP KVMs or hardware remote-access cards, SUSE Linux Enterprise Server bundles remote installation methods such as