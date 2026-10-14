
![](img/f7cef0df22f9dba5a41777808c98eece_150_0.png)

Figure 7-16: USB storage devices

## Working with Bluetooth Devices

While we’re on the topic of file handling, it is probably a good time to learn how to work with Bluetooth devices. As I mentioned in Chapter 3, if you have a Bluetooth adapter in your machine, either built in or plugged into a USB port, a Bluetooth icon will appear in the right half of the GNOME upper panel.

## Pairing Devices

Before you can transfer files between your Bluetooth devices, you need to pair them. This is how you do it:

- 1. Click the Bluetooth icon in the top panel, and select Set up new device.
- 2. In the Bluetooth setup wizard that appears, click Forward.
- 3. Ubuntu will then search for Bluetooth devices in the vicinity of your computer. Once it discovers a device, that device will appear in the center pane of the window, as in Figure 7-17. Once the device you want to pair to appears, click it, and then click the Forward button.
- 4. In the next page of the wizard, a personal identification number (PIN) will appear (Figure 7-18). An input window should also then appear in the Bluetooth device you’re trying to connect to. Input the PIN into that input box.
- 5. Assuming the pairing is successful, the final page of the wizard will then appear. Click Close to complete the pairing process.

## Device search

Select the device you want to set up

Searching for devices...

| Device | Type |
| --- | --- |
| RG Phone | Phone |

Show Only Bluetooth Devices With...

Device type:

All types

PIN options...

Cancel

Back

Forward

Figure 7-17: Searching and selecting nearby Bluetooth devices in Ubuntu

## Device Setup

Please enter the following PIN on 'RG Phone':

948968

Cancel

Figure 7-18: The Bluetooth wizard provides you with a PIN to input into the device you're pairing to.

## Sending Files by Bluetooth

To send a file by Bluetooth from your computer to another Bluetooth-capable device, click the Bluetooth panel icon, and select Send files to device. A window will then appear in which you can navigate to the target file. Once you have made your selection, click Open. The Select Device window will then appear (Figure 7-19). Select the recipient machine, and click Send to. Your machine will then begin transferring the file. If the recipient machine is set up to seek permission first before accepting a Bluetooth file transfer, you or the recipient will have to perform the appropriate action on the recipient machine before the transfer can be completed.

![](img/f7cef0df22f9dba5a41777808c98eece_152_0.png)

Figure 7-19: Selecting paired Bluetooth devices to receive sent files

## Receiving Files by Bluetooth

To receive files via Bluetooth from another Bluetooth-capable device, you have to first set up your device to allow such transfers. To do this, click the Bluetooth panel icon, and select Preferences. In the Bluetooth Preferences window, click the device you want to set up, and then click Receive Files. A Personal File Sharing Preferences window will then appear. In that window, check the box next to the words Receive files in Downloads folder over Bluetooth. For your safety, select Only for set up devices in the drop-down menu button to the right of the words Accept files. Your window should then look like that in Figure 7-20. If so, click Close. Your machine will then automatically receive files sent to it via Bluetooth and save them to the Downloads folder.

## Backing Up Your Files

Figure 7-20: Setting up your system to receive files sent from other Bluetooth devices.

You’ve worked hard to accumulate all of your files. Hours of typing, hundreds of photos, piles of music CDs—it’s all there on the hard disk. So, what happens to it if something goes wrong with your computer? In many cases the answer is, unfortunately, that all of the data is lost forever. To save you the pain of this experience, it’s a great idea to make regular backups.

Plenty of backup utilities are available, but Déjà Dup stands out to me as being the easiest to use. Open the Ubuntu Software Center, and install the Déjà Dup Backup Utility. It’ll put itself in the System Tools section of the Applications menu, so head over there and start it up.

Now is a good time to decide what you’re going to use to store your backups. I have an external USB hard disk that does the trick, but you can use a USB flash drive, recordable CD or DVD, or even a web server. I wouldn’t recommend putting your backups on the same computer, though. The best policy is to put some distance between the original files and the backups, so if there’s a fire or some other disaster, you’ll have at least one copy of them left intact. Make sure you have enough space for the backup too; regular CDs are only 700MB, but my Pictures folder alone weighs in at whopping 4.3GB!
