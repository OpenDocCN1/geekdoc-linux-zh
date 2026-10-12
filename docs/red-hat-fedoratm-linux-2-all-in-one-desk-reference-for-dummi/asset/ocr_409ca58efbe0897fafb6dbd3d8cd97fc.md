5. **Press Enter twice.**  
Minicom returns to the configuration menu.

6. **Select Save setup as dfl and press Enter.**  
Minicom saves the settings.

7. **Select Exit and press Enter.**  
Minicom returns to online mode.

8. **Press Ctrl+A and X.**  
Minicom prompts you to ask whether you really want to exit.

9. **Press Enter to exit.**  
After setting the correct device name for the serial port where the modem is connected, make sure that your modem is powered on and connected to the phone line.

10. **Start Minicom again (type minicom in the terminal window).**

11. **Press Ctrl+A to get the attention of the Minicom program.**  
After you press Ctrl+A, if you press Z, a help screen appears in the form of a text window. In the help screen, you can get information about other Minicom commands.

12. **From the help screen, press Enter to go back to online mode.**  
In online mode, you can use the modem’s AT commands to dial out. In particular, you can use the ATDT command to dial the phone number of another modem (for example, dial your ISP’s number). When you get the login prompt, you know that the modem is working. Figure 1-9 shows the results of a typical dial-up using Minicom. The line that says Connect 38400 indicates that it’s a 38.4 Kbps connection. Only 38.4 Kbps with a 56 Kbps modem. (No wonder I needed DSL or a cable modem!)

![](bbox=[0.15, 0.69, 0.68, 0.93])