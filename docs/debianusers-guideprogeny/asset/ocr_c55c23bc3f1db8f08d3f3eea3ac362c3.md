# The apt-cdrom Command (Sets Sources)

| Option | Action | Comment |
| :--- | :--- | :--- |
| ▼ -a<br>▼ --throug h | Scan for packages. | May not be needed for all CDs. |
| ▼ -d<br>▼ --cdrom | Sets the CD mount point. | The mount point must be listed in /etc/fstab.<br><br>The equivalent option in the configuration file is:<br><br>Aquire::CD::mount |
| ▼ -f<br>▼ --fast | Copies files to your system without checking them. | The equivalent option in the configuration file is:<br><br>APT::CD::Fast |
| -o GROUP TOOL=OPTION | Edits an option in the configuration file. | The configuration file is /etc/apt/apt.conf.<br><br>See the configuration file and on-line help for information about options. |