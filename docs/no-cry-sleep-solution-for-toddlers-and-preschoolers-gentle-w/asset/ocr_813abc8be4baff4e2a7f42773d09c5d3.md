You can combine the q option with the i or l option to display information about the package. The option -qi displays information about the software, such as the version number or author (-qpi queries an uninstalled package file). The option -ql displays a listing of all the files in the software package. The --h option provides a complete list of rpm options. Common query options are shown in Table 29-4.

> Tip Keep in mind the distinction between the installed software package name and the package filename. The filename ends in a .rpm extension and can only be queried with a p option.

To display information taken directly from an RPM package, you add the p qualifier to the q options as shown in Table 29-5. The -qpi combination displays information about a specific package, and -qpl displays a listing of the files a given RPM package contains. In this case, you must specify the entire filename of the RPM package. You can avoid having to enter the entire name simply by entering a unique part of the name and using the * filename-matching character to generate the rest.

If your RPM query outputs a long list of data, like an extensive list of files, you can pipe the output to the more command to look at it screen by screen, or even redirect the output to a file.

```
# rpm -ql mozilla | more
# rpm -qpl emacs-21.2-18.1386.rpm > mytemp
```

# Installing and Updating Packages with rpm

You use the -i option to install new packages and the -U option to update currently installed packages with new versions. With an -e option, rpm uninstalls the package. If you try to use the -i option to install a newer version of an installed package, you will receive an error saying the package is already installed. When a package is installed, RPM checks its signature, using imported public keys from the software vendor. If the signature check fails, an error message is displayed, specifying NOKEY if you do not have the appropriate public key. If you want to install over an already installed package, you can force installation with the --replacepkgs option. Sometimes a package will include a file, such as a library, that

TABLE 29-4
Query Options for Installed Software
| Option | Meaning |
|---|---|
| -q application | Checks to see if an application is installed. |
| -qa application | Lists all installed RPM applications. |
| -qf filename | Queries applications that own filename. |
| -qR application | Lists applications on which this application depends. |
| -qi application | Displays all application information. |
| -ql application | Lists files in the application. |
| -qd application | Lists only documentation files in the application. |
| -qc application | Lists only configuration files in the application. |