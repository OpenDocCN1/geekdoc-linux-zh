# CHAPTER NINE: CUSTOM SCRIPTS

I have explained a lot of ways in which you can harden and sanitize your new Linux machine. Everything up to this chapter relies on manual configuration. Next, let's automate a lot of the daily or weekly tasks by creating our own Linux maintenance script. I respect that some readers may just want to download a pre-configured script and use it right away. The following commands within Terminal will download the script, make it executable within your Linux machine, download the shortcut file, and move both to create a "Maintenance" shortcut in your "Applications" menu. The rest of the chapter explains how to create your own.

```
wget https://inteltechniques.com/data/maintenance.sh
chmod +x maintenance.sh
wget https://inteltechniques.com/data/maintenance.desktop
sudo mv maintenance* /usr/share/applications/
```

The text on the following page displays the entire script. It identifies the file as a bash script; clears the screen; and presents a menu with seven selectable menu options. The image below displays the script once it is finished and executed. You would enter the number associated with the feature you want to execute and strike the Enter key. Striking the Enter key at any prompt without a number presents the original menu again. Each option correlates to the commands previously presented throughout this guide. If you wanted to modify this script, you would choose option "6" to launch a file viewer with admin rights and navigate to /usr/share/applications and edit the maintenance.sh file.

![](bbox=[0.15, 0.48, 0.84, 0.64])

Now, let's understand how we could have built this manually. Copy the entire code presented within the next page in Courier New 11-point font and paste the text into a new file saved as maintenance.sh within your Documents folder using the Text Editor application on your own Linux machine.

```
#!/bin/bash
clear
COLUMNS=12
PS3='Selection: '
options=(
"Show Hidden Files"
"Hide Hidden Files"
"Start NextDNS"
"Stop NextDNS"
"Restart NextDNS"
"Launch Files with Admin"
```