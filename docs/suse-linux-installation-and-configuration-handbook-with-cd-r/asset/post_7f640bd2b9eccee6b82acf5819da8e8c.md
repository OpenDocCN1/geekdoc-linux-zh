
11. Finally, you must set the Resolution in DPI option. This is the printing resolution in dots per inch. Usually, you would get this value from your printer's manual because it differs from one printer to the other. The default of 300×300 is a safe choice in case you are not sure of what to enter here.

12. Choose Install and press Enter to install your printer. YaST will pop up a window displaying the status of the configuration (see Figure 11.3).

FIGURE 11.3
YaST displays the status of the configuration.

![](img/659f91d9da7b29976c0625e2e9628511_255_0.png)

Now you have successfully installed your printer. You must do one last thing, though—make sure that the printing service is running. To do that, log in as root and run this command:

```
# /etc/rc.d/lpd restart
```

You won't need to do this again; it will be done automatically for you on every system boot up.

The printer has been installed with the name lp. We are sure that you can't wait to try it out! The simplest way is by trying to print a file from the command line. To do that, you can use the lpr command like this:

```
$ lpr file.txt
```

The contents of file.txt should be printed to your printer. If you want to try something a little more difficult than a text file, you can print from Netscape Navigator.

Your printer is now called lp, so you need to tell applications to print to that name.

## Printing to a Remote UNIX Printer

If your machine is part of a network, there is a good chance that somewhere out there exists a printer you can use. This printer is considered a network printer that can be shared by more than one machine. This sure beats having to buy a printer for every machine.

You easily can set up your SuSE Linux box to print to another printer on the network. YaST enables you to do this easily. To have SuSE Linux print to a remote UNIX printer, follow these steps:

- 1. Log in as root.
- 2. Run YaST.
- 3. Navigate to System Administration, Network Configuration, Administer Remote Printers and press Enter.
- 4. A dialog window pops up—this is where you will define the remote printer (see Figure 11.4).

### FIGURE 11.4

Configuring remote printers with YaST.

![](img/659f91d9da7b29976c0625e2e9628511_256_0.png)

- 5. The first field is the Name of Printer field. You have two choices here, you can either change one of your existing printer configurations to a remote configuration, eliminating the need to adjust the rest of the system to the new configuration. Or you can create a totally new printer configuration for the remote printer. To choose an existing configuration, press F3. A window will pop up showing you a list of the entire current printer configuration on your system; select the one you want to change and press Enter. If you are going to define a new configuration, just enter its name here—for example, remotprinter.
- 6. Press Enter or Tab to move to the next field—the Spool Directory field. As you can see, YaST already has entered a default choice there for you. This is the directory that SuSE Linux will use to hold the files that are to be printed until the remote printer is able to process them. We recommend leaving the default value as it is. Press Enter to move to the next field.
- 7. The next option is where you enter the Server Name. That can be a fully qualified domain name—printer.company.com for example—or the IP of the server to which the remote printer is connected. You can ask your system administrator for this information if you don't know it.
- 8. Finally, the last field is the Name of Printer on Server option. This is the name of the printer as it is configured on the remote server. The default is usually lp, but you should make sure by asking your system administrator or the person who configured that machine.
- 9. Press F4 to apply your new configuration. YaST will attempt to verify that the server name you entered does exist. If it can't reach it, it will warn you. You can, of course, force your configuration even if YaST complains about not finding the server.

Now you are finished with the remote printer configuration. If you have created a new printer name, you will have to tell your applications about it when you want to use it. If you have changed an already existing configuration to be a remote one, you won't need to change anything else. You should note, however, that you must inform the administrator of the remote printing machine that you want to use his printer. This way he will add the name of your machine to his /etc/hosts.lpd file to allow your machine to pass print jobs to his print spooler.

## Printing to a Remote Microsoft Windows Printer

The previous section assumed that the network printer is connected to a UNIX machine, but what if the network is Microsoft Windows-based? That means that the printer will most likely be connected to a Windows-based PC. Printing to such a printer is easy. All the print jobs will be sent to the Windows printing system using Samba. All this can be configured using YaST.

You should, however, have a working Samba configuration to successfully print to the Windows machine. Refer to Chapter 15, "Connectivity with Windows Through Samba," to learn how to set up Samba properly.

To configure your SuSE Linux box to print to a remote Windows printer using Samba, follow these steps:

- 1. Log in as root.
- 2. Run YaST.
- 3. Navigate to System Administration, Network Configuration, Connect to Printer Via Samba and press Enter.
- 4. The configuration module pops up. If you have an existing printer configuration, YaST will ask you whether you want to overwrite it or append to it (see Figure 11.5). If you are not planning to use your old settings, just overwrite them. If you want to keep your old settings and append the Samba printer configuration to them, choose Append.

### FIGURE 11.5
YaST has detected that you already have a printer configuration. Should you overwrite it or append to it?

![](img/659f91d9da7b29976c0625e2e9628511_257_0.png)

- 5. The first option, Color Printer, asks whether you have a color printer or not. Check this option by pressing the space bar if you do have a color printer. Press Tab to proceed to the next option.
- 6. In the Printer Type option, you will be presented with three choices: PostScript Printer, HP Deskjet, and Other Printer. Make your choice according to the type of printer you have. Press Enter to select one. You will be automatically moved to the next option.
- 7. This option is the Printer Name. Depending on what you chose in the previous option, you will be presented with a list of printers compatible to the category you selected. Find your printer model or one that is compatible with yours and press Enter.
- 8. The Paper Format option sets the size and format of the paper you are going to be using. Most people use A4 paper, so you might want to select that one.
- 9. The Server Name field is where you will enter the name of the Windows machine to which the printer is connected. This is its name as defined on the Windows network.
- 10. The Name of the Printer Service option is the name of the printer on that machine. This can easily be found out by browsing the Windows machine from the Network Neighborhood. The printer name is the name under the printer icon. According to Figure 11.6, this would be GOGEIIite.

### FIGURE 11.6
You can get the name of the printer to which you want to connect from the Network Neighborhood on Windows.

![](img/659f91d9da7b29976c0625e2e9628511_258_0.png)

- 11. If the printer requires a User Name, enter it here.
- 12. Finally, if the printer requires a Password, enter it here.
- 13. Choose Install and press Enter to install your remote printer configuration.

That's it; you are all set to print to the remote Windows printer thanks to Samba and YaST. All your printing jobs will be sent to the Windows print system over the network.

## Printing to a Remote Printer Over a Novell Network

If your SuSE Linux box is part of a Novell Network, you still can use a remote printer. The configuration process is similar to the one you used in the previous section. YaST makes life very easy, especially when it comes to printing.
