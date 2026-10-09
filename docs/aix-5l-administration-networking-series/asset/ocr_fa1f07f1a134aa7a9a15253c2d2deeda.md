If any of the listed products are missing, you need to install the packages from the AIX installation media. Do not forget to reinstall the patch set for the current maintenance level in case modifications have been made. The maintenance-level code is installed by using the SMIT FastPath smitty update_all.

On the next screen, you are prompted for the location of the maintenance code; for example, if it is located on a CD-ROM inserted in /dev/cd0, then enter the device name. If the code is located in /usr/sys/inst.images, then enter the system path. If you do not want to commit the software updates, but instead install the patch set in an applied state, follow this procedure: in the SMIT panel set the COMMIT Software Updates? field to No, and set the SAVE Replaced Files? field to Yes. Then press the ENTER key twice to install the software.

# ## Red Hat Package Manager (RPM)

Before installing the whole AIX Toolbox for Linux, you must first install the Red Hat Package Manager (RPM). This filesset must be installed as a traditional AIX filesset using installp, SMIT, or WebSM. The quickest method is to use installp on the command line. First, change directory to the CD-ROM mount point, for example, /cdrom. In this case, you need to change directory to the installation directory /cdrom/INSTALLP/ppc. Use the following installp command:

```
```bash
# cd /cdrom/INSTALLP/ppc
# installp -qacXg -d . rpm.rte
```
```

or use the SMIT FastPath smitty install_latest

On the first SMIT screen, you are prompted for the location of the code to install. If your CD-ROM is mounted as /cdrom, use the path /cdrom/INSTALLP/ppc. You can leave the Software To Update field set to _update_all, since the RPM package is the only filesset in this directory.