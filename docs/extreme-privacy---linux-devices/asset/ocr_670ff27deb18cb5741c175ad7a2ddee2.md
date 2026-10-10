```
"Apply Updates" )
select opt in "${options[@]}"
do
case $opt in
"Show Hidden Files")
gsettings set org.gnome.nautilus.preferences show-hidden-files true
gsettings set org.gtk.Settings.FileChooser show-hidden true
;;
"Hide Hidden Files")
gsettings set org.gnome.nautilus.preferences show-hidden-files false
gsettings set org.gtk.Settings.FileChooser show-hidden false
;;
"Start NextDNS" )
nextdns start
;;
"Stop NextDNS" )
nextdns stop
;;
"Restart NextDNS" )
nextdns restart
;;
"Launch Files with Admin" )
sudo nautilus
;;
"Apply Updates")
sudo apt update
sudo apt upgrade -y
sudo apt full-upgrade -y
pop-upgrade release upgrade
sudo apt autoremove -y
sudo apt autoclean -y
flatpak update -y
;;
esac
done
```

This is a fairly basic Bash script, but let's walk through each piece to understand the functionality for future replication.
#!/bin/bash: This first line is known as a 'she-bang'. It identifies the text file as a script of commands to be executed.
clear: This command simply clears the screen in order to present a clean menu. While not necessary in this script, I prefer to clear the screen before presenting any content. This eliminates any other text which may be confusing to the viewer.
COLUMNS=12: This command displays the contents within a column. It prevents the menu choices from being displayed as a single horizontal line. You can modify this number if your menu items do not fit as desired.