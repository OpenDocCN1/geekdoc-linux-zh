# ## Network use

# Are these tools good for only imaging local disks and partitions?

Y ou can use **Clonezilla** for multicast cloning via two available options. **Clonezilla Server Edition** requires setting up a Diskless Remote Boot in Linux (DRBL) server to broadcast images across the network. On a smaller network, you can use the **Clonezilla Lite Server** mode on the bootable CD to set up a temporary server.

You use **Clonezilla** to save the cloned image of a disk or individual partitions on the network. For this it can establish a connection to the remote machine via SSH, or through an SMB, NFS or WebDAV server.

Similarly, in addition to creating and restoring local images, **G4L** also has impressive network capabilities. You can use it to backup/restore and image to/from a remote machine on the network via various mechanisms, including FTP and UDPcast. To use the latter, configure the Live environment to set up one machine as a multicast server, which then broadcasts images stored locally or elsewhere on the network.

Unlike the other tools on test here, **FOG Project** is built from the ground up to work over the network. It works best when it doubles up as the DHCP and PXE server. All of FOG Project’s imaging tasks, including capturing and deployment, are handled remotely over the network. Unlike the other solutions it forces the use of a lot

![](bbox=[0.51, 0.09, 0.93, 0.24])

> You can use the G4L Live CD to turn remote computers into receivers that’ll pull the broadcasted images and restore them over the network.

more network services such as DHCP and PXE servers, which are optional with the other tools. By contrast, neither **Deepin Clone** nor **WereSync** offer any network awareness of their own. With **Deepin Clone**, though, you could obviously mount a remote computer in the local filesystem and point to it as the destination for saving the image of a local disk/partition.

# VERDICT

| | **CLONEZILLA** | | **G4L** |
|---|---|---|---|
| | 8/10 | | 8/10 |
| **DEEPIN CLONE** | 5/10 | **WERESYNC** | 1/10 |
| **FOG PROJECT** | 9/10 | | |

FOG Project is designed from the ground up to reside on the network, while Clonezilla and G4L can be used to work across the network as well.

# ## Deploying images

# Putting the cloned images to use.

W e wouldn’t fault you for thinking that the process for restoration would be the reverse of the imaging process for each of the tools. But **Deepin Clone** and **WereSync** will surprise you in this respect.

**Clonezilla** has a very straightforward process for restoring a partition or an entire disk from a cloned image. You begin by first selecting the repository that houses the cloned images. Next, Clonezilla displays a list of all the unmounted partitions to which you can restore the image.

After you’ve made your selection, **Clonezilla** wipes the partition and creates a new partition table on the disk, so be careful with this. Also keep in mind that the destination partition needs to be equal to or larger than the source, as it can’t restore an image to smaller disks.

When restoring with **G4L**, you must point the tool to the saved image, followed by the location of the disk or partitions where you want to restore the image. During our tests, while G4L certainly began restoring a cloned image from a larger disk to a smaller one, the process never completed successfully. On the other hand, attempts at restoring images of a smaller disk to a larger one went more smoothly.

With **FOG Project**, you first need to register the target machine with the server and then associate a cloned image with it. To do the actual rollout, you’ll have to create a deploy image task before the image is rolled over to the machine via PXE. The same process works irrespective of whether you wish to deploy to a single computer or multiple ones.

![](bbox=[0.51, 0.55, 0.93, 0.7])

> All tools can perfectly restore a smaller image to a larger disk, but only WereSync promises to restore a larger image to a smaller disk.

To restore an image with **Deepin Clone**, all you have to do is point the app to the image file along with the disk or partition you want to restore it to. As with its cloning process, the restoration doesn’t offer any configurable options.

By default, **WereSync** directly clones a drive to another, so there’s no option for restoration. However, you can force the app to image a drive by changing the destination to an IMG file. To restore from the image, you’ll have to reverse the fields and specify the IMG file as the source.

# VERDICT

| | **CLONEZILLA** | | **G4L** |
|---|---|---|---|
| | 8/10 | | 8/10 |
| **DEEPIN CLONE** | 5/10 | **WERESYNC** | 5/10 |
| **FOG PROJECT** | 9/10 | | |

They’re all well-matched, with the exception of WereSync and Deepin Clone.