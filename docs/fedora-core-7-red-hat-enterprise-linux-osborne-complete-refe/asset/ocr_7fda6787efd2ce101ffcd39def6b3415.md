A complete description of **rpm** and its capabilities is provided in the online manual:

```
# man rpm
```

# Querying Information from RPM Packages and Installed Software

The **-q** option tells you if a package is already installed, and the **-qa** option displays a list of all installed packages. Piping this output to a pager utility, such as **more**, is best.

```
# rpm -qa | more
```

In the next example, the user checks to see if emacs is already installed on the system. Notice the full filename of the RPM archive is unnecessary. If the package is installed, your system has already registered its name and where it is located.

```
# rpm -q emacs
emacs-22.0.95-1
```

You can combine the **q** option with the **i** or **I** option to display information about the package. The option **-qi** displays information about the software, such as the version number or author ( **-qpi** queries an uninstalled package file). The option **-qI** displays a listing of all the files in the software package. The **--h** option provides a complete list of **rpm** options. Common query options are shown in Table 29-4.

> **TIP** Keep in mind the distinction between the installed software package name and the package filename. The filename ends in an .rpm extension and can only be queried with a p option.

To display information taken directly from an RPM package, you add the **p** qualifier to the **q** options as shown in Table 29-5. The **-qpi** combination displays information about a specific package, and **-qpl** displays a listing of the files a given RPM package contains. In this case, you must specify the entire filename of the RPM package. You can avoid having to enter the entire name simply by entering a unique part of the name and using the * filename-matching character to generate the rest.

| Option | Meaning |
| :--- | :--- |
| -q application | Checks to see if an application is installed. |
| -qa application | Lists all installed RPM applications. |
| -qf filename | Queries applications that own *filename*. |
| -qR application | Lists applications on which this application depends. |
| -qi application | Displays all application information. |
| -qI application | Lists files in the application. |
| -qd application | Lists only documentation files in the application. |
| -qc application | Lists only configuration files in the application. |

**TABLE 29-4** Query Options for Installed Software