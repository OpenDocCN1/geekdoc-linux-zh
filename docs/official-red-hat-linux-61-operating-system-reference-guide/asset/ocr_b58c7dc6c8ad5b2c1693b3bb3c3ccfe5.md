Enter the complete phone number for the remote machine, and make sure to include any numbers required to access outside lines.

For example, if you need to dial 9 and then the number, and the computer you’re connecting to has a telephone number of 555-0111, then you’d enter 95550111.

The next information you’re asked for is the modem port. This is a drop down box of available ports. If you’re using a dual-boot Linux/Windows system and you know the COM port your modem is on, the following map may be of use:

Map to Windows COM ports are as follows:

+   * `ttyS0` -> COM1: under MS-DOS;
+   * `ttyS1` -> COM2: under MS-DOS;
+   * `ttyS2` -> COM3: under MS-DOS;
+   * `ttyS3` -> COM4: under MS-DOS.

The login name is the one for the PPP account. The password you enter will be shown in plain text, so be careful who you have around when you enter it! If you will be using PAP authentication, check the box: when you’ve entered the other required information, select the Customize button at the bottom of the screen.

If you’re using PAP, select the PAP tab and enter your username and then the secret the ISP has provided you in the Secret field. The other defaults should be sufficient, but if you need to, you can edit the initial settings using the Customize option.

# Modifying a PPP or SLIP Configuration

You can edit an existing configuration as well as delete it by selecting it from the list on the PPP/SLIP/PLIP configurations screen.

+   * Open Config => Networking => Client tasks => PPP/SLIP/PLIP.
+   * You will then be presented with the PPP/SLIP/PLIP configurations screen (see Figure 3–13, *PPP/SLIP/PLIP Configurations Screen*). Select the configuration you would like to modify or delete.

This will open the appropriate interface screen for your configuration. If you wish to delete the configuration, select Del at the bottom of the screen. The Modem port is on the Hardware tab and is a drop down menu. If you want to change the