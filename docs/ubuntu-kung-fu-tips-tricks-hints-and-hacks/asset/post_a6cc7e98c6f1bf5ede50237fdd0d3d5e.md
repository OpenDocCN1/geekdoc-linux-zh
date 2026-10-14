
address range). This can be useful in the case of shared folders, for example, where other computers in your workplace or home may wish to access files on your computer.

Here are the steps required to create an in-bound rule:

- 1. Start the Firestarter configuration program, if it isn't already running, by clicking System ⇨ Administration ⇨ Firestarter. You'll need to type your password when prompted.
- 2. Click the Policy tab in the program window, and ensure Inbound Traffic Policy is selected in the Editing dropdown list.
- 3. Under the Allow Service heading in the lower-half of the program window, right-click and select Add Rule from the menu that appears.
- 4. In the dialog box that appears, select from the Name dropdown list the type or program that you'd like to allow through the firewall. For example, to allow BitTorrent connections, select that in the list. To let others access shared folders on your computer, select Samba (SMB). Note that the Port field will be automatically filled in once you make your selection. You can edit this if you wish, but there should be no need.
- 5. If the rule relates to inbound connections from the Internet, ensure the Anyone radio button is selected under the When The Source Is heading.
- 6. To limit the type of incoming connection to the local network, and not the entire Internet, click the IP, Host or Network radio button. You'll then need to find out the network range that your computer is part of. To do so, right-click the NetworkManager icon at the top-right of the screen, and select Connection Information. Look in the IP Address line within the dialog box that appears, and make a note of the first three numbers. On my test PC, this line read 192.168.1.5, so I made a note of 192.168.1.
- 7. Back in Firestarter's rule creation dialog box, type the numbers, followed by a period, then a zero. So, in my case I typed 192.168.1.0. Then add a forward slash, and type 24. On my test PC the entire line read 192.168.1.0/24.
- 8. Once done, click the ADD button, and then the APPLY POLICY button on the toolbar. Then close Firestarter.

malware for Linux at the present time. There's some debate about whether this will change in future, but right now an Ubuntu user is quite simply safe from viruses. No further action is required.

However, aside from guarding against future threats, installing an anti-virus program allows you to watch out for Windows or even Mac viruses in files sent to you. Therefore, you can avoid passing on virus-infected files that might affect those running non-Linux operating systems.

> **TIP** Why not convert your friends or colleagues to using Ubuntu? The fact Ubuntu is immune to viruses is a very persuasive argument in its favor. If you do convert them, be sure to suggest they get a copy of *Ubuntu Pocket Guide and Reference* to help them get started!

There is a variety of commercially sold antivirus programs for Linux, but perhaps the best choice from an open source perspective is ClamAV. This is industrial-strength antivirus designed for server computers, but you can also install ClamTK, a small program that provides a graphical front end, and thereby makes ClamAV suitable for more humble users.

## Installing ClamTK

Start Synaptic and search for `clamtk`. Put a check alongside the `clamtk` entry in the results, and click Mark for Installation in the menu that appears. Agree to install the list of dependencies, that includes ClamAV itself, and then click the APPLY button on the toolbar.

When ClamTK is run for the first time it’s necessary to update the virus database. In future this will be done automatically and periodically in the background, without any need for user intervention.

To manually update the database, ClamTK needs to run as root user, so open a terminal window (Applications → Accessories → Terminal), and type the following:

- - `gksu clamtk`

Click Help → Update Signatures. Once ClamTK reports the signatures are up to date, close the program window.

> **TIP** You can update the virus database at the command-line by typing `sudo freshclam`. Don't worry if, while doing this, you see a warning that ClamAV is out-of-date—this simply means that the version offered in the Ubuntu repositories is lagging a little behind the main releases. This is not an issue.

## Scanning for viruses

To start ClamTK, click Applications → System Tools → Virus Scanner.
