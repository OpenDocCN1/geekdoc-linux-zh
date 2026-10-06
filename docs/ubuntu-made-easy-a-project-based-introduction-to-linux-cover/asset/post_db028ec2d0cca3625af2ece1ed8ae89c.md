
the window and then click the Print Test Page button (Figure 10-1). If the test page looks normal (something like Figure 10-2), everything should be fine, and you can close the Printer Properties and Printing windows.

![](img/d35fa962e6f9664d66dc83916f426418_218_0.png)

Figure 10-1: Printing a test page with your new printer via the Printer Properties window

![](img/d35fa962e6f9664d66dc83916f426418_218_1.png)

Figure 10-2: An Ubuntu test page

If you have a printer that plugs into your computer's parallel port, auto-detection and setup should also work if the printer was connected when you turned on the computer. If it was not, shut down your system and turn your computer off, connect your printer to the computer, and then start your printer again. With luck, your printer should be recognized and set up automatically this time around. You can also try this approach with a USB printer that was not recognized initially.

## Manually Configuring Printers

If your printer isn't automatically recognized, you can still set things up manually. I'm assuming you have a printer that connects to your computer with a cable of some description, either USB or parallel. If you have a wireless-enabled printer, or one that's connected to your local network, skip to one of the next two sections for instructions. But for the cable-enabled among you, here's what you need to do:

- Click the power button on the top panel and select Printers from the menu that appears. Either a Printing window will appear, showing the printers that have already been recognized, or a message will tell you that no printers have been configured.

- Click the Add button, after which the system will show any new finds in a New Printer window (Figure 10-3).

![](img/d35fa962e6f9664d66dc83916f426418_219_0.png)

Figure 10-3: Setting up a printer manually

- 3. Click the entry for your printer in the left pane of that window and then click Forward. The system will begin searching for drivers for your printer.

- 4. If your printer is supported, the next page or two of the wizard will ask you to enter some basic details about the printer. These might include its name and model, for example. Fill in the blanks to suit your needs and then, when you go to the last page, click Apply.

- 5. The wizard will close, and you'll be asked whether you would like to print a test page. Make sure that everything is correct, it is always a good idea to print a test page, click Yes.

Your system will send a document to your printer and let you know it has done so in a small window, which you can close. The printer should print the test shortly.

**NOTE** If your test page didn't come out the way or if your printer was not configured automatically by the system, check out http://www.openprinting.org/printers/ to see whether there are any special requirements or caveats for your model.

## Setting Up Wireless-Enabled Printers

Printers with built-in wireless (Wi-Fi) adapters are becoming increasingly common. You normally have the choice of connecting in the traditional way, using a USB cable, or by setting them up to connect to your wireless network. In the latter case, any computer that is also connected to the network can access the printer. Neat, huh? If you have such a printer and would like to make use of its wire-free capabilities from your Ubuntu machine, read on:

- 1. Make sure that the printer is turned on and connected to your wireless network. Exactly how you do this varies depending on the machine and model of printer, so check out the printer's manual for instructions.

- 2. You'll need to get a couple of vital pieces of information about the printer's wireless network settings before you can continue. In particular, you are looking for its IP address. The printer will probably have a way of displaying this, either through a small built-screen or by printing out an information page. Check the printer for details.

- 3. With the printer's IP address in hand, get back in front of the Ubuntu computer and click the power button on the far right of the top panel. Select **Printers** from the menu that appears, and a Printing window will appear.

- 4. Click the **Add** button, after which the New Printer window will appear.

- 5. Select **Network Printer ▸ Find Network Printer** in the left pane of that window by clicking that entry once. Now, enter the printer's IP address into the Host box, as shown in Figure 10-4. (Note that your printer's IP address will probably be different from the one you here.)

![](img/d35fa962e6f9664d66dc83916f426418_221_0.png)

Figure 10-4: Connecting to a wireless-enabled printer

- 6. Click **Find**. After a little while, your computer should find the printer, and you will be taken to a page where you can specify information about its make, model, and so forth.

- 7. Now continue from Step 4 in “Manually Configuring Printers” on page 182.

Unfortunately, some wireless printers are a little fiddly to set up in Ubuntu, so the instructions above might not work. You may need to install extra software or a slightly different type of “network printer” configuration than the one I discussed. If you suspect your printer might be one of the awkward ones, try the Ubuntu Forums at http://www.ubuntuforums.org/ to see if else has figured out how to set it up. And of course, if nothing seems to work, you can always fall back on using a USB cable.

## Setting Up Printers Connected over a Network

If you want to use a printer connected via a home or office network, just follow these steps:

- 1. Click the power button on the far right of the top panel and select **Printers** from the menu that appears. A Printing window will appear, showing the printers that have already been recognized and/or configured.

- 2. Click the **Add** button, after which the New Printer window will appear.

- 3. Select Network Printer Windows Printer via SAMBA in the left pane of that window by clicking that entry once and then click the Browse button.

- 4. In the SMB Browser window that appears (Figure 10-5), navigate your way to the printer you want. Sometimes it takes a while for the information to load, so hang tight if things seem to stalled. When you find the printer you're looking for, select it and then click OK. Once you're in the New Printer window, click the Forward button.

- 5. Now continue from Step 4 in “Manually Configuring Printers” on page 182.

![](img/d35fa962e6f9664d66dc83916f426418_222_0.png)

Figure 10-5: Browsing for printers connected over a Windows network
