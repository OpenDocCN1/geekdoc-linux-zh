![](bbox=[0.05, 0.06, 0.5, 0.19])

Figure 10.5 Add Host dialog window.

badly formatted data and the software will accept it without any warnings.

In practice, most, if not all, UNIX configuration files (including `/etc/hosts`) don’t normally have any built-in mechanisms to ensure that the information entered is indeed correct. Many files, however, do provide some sort of error-checking to pinpoint specific format- or syntax-related errors. This is usually accomplished by running the associated program that is responsible for parsing the specific configuration file and operating on its contents to provide some specific application or system service. Only at this point are any errors detected. The control panel software does provide a rudimentary check; for a valid entry to be accepted, the first and seconds fields must be filled in, while the third is optional and can be left blank.

Once the desired information has been entered, the user must click the Done button. This action will add the entry to the list of existing host mappings. However, the user must save the new configuration by selecting the Save button. If the user doesn’t save the new entry and exits the control panel, the new entry will be lost. Unfortunately, the software doesn’t provide a warning if the user decides to exit the software before saving the new host configuration.

To alter an existing host entry, select it from the main window and click the Edit button. The same window shown in Figure 10.5 will be displayed, but it will already include the host information. Change the desired information and click the Done button. If a host is to be deleted from the list, simply select it and click the Remove button.

If you want to really make sure that the entry was added correctly, just use the grep command and search for the new hostname from the `/etc/hosts` file. Thus,