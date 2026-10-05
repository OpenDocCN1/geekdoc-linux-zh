# System Service Tools
CHAPTER 6

TABLE 6.1 YaST Command-Line Options
| Task or Desired Action | Option |
|---|---|
| Quit after first mask | -autoexit |
| Redirect output to a terminal | -terminal |
| Save debugging info to debugfile | -debugfile |
| Security settings and configuration | -mask security |
| Select a keymap | -mask keymap |
| Select language | -mask language |
| Select the boot Linux kernel | -mask kernel |
| Set a console font | -maskconsolefont |
| Set hostname | -mask name |
| Set SDN-specific config parameters | -mask isdn-num |
| Set system's CD-ROM drive | -mask cdrom |
| Set the timezone | -mask timezone |
| Show help | -mask help |
| Update a SuSE system | -mask update |
| Use a new configuration | -plain |

Log in as the root operator, start the yast program from the command line with the following code and press the Enter key:

# yast &

If you're running X, the program's main window will appear as shown in Figure 6.1.

![](bbox=[0.058, 0.611, 0.783, 0.803])

If you manually configure your system's services by hand-editing configuration files, be careful—making changes to default values in /etc/initabb or indiscriminately using