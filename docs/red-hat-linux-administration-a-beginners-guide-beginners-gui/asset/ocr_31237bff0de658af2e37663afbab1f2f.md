| Option | Description |
| --- | --- |
| -v URI | Specifies the device back end in URI form. |
| -u allow|deny:user, user | Changes user permissions for the printer. (See Critical Skill section 19.8 on setting user permissions.) |
| -vd printername | Changes the default printer to the one specified. |
| -x printername | Deletes the named printer. |
| -E | Starts the printer and sets it to accept print jobs. |

An example is in order to show how this works, but before we get to that, let's introduce a couple of other useful commands. The `lpinfo` command is closely related to adding and modifying printers with `lpadmin`. When using the web interface you will be presented a list of options for printer model and back-end device. Using the command line, you may not be sure which models and devices are supported on a particular setup. The `lpinfo` command can list for you the models and devices that a particular server supports. Specifying the `-m` option to `lpinfo` will list the models (in the form of a path to the `.ppd` file) that you can pass to `lpadmin`'s `-m` option. Likewise, specifying `-v` to `lpinfo` will list the back-end devices available to pass to `lpadmin`'s `-v` option.

The `lpstat` command can be used to gather information on configured printers, classes, and pending print jobs. There are a number of options for selecting what output is returned from `lpstat`, and the man page will tell you all about them, but for our purposes we're just going to use the `-s` option. Using `lpstat` with the `-s` option will list the classes and printers that have been set up, along with the devices associated with each printer and will tell you which printer is the default. It's worth mentioning that the `-t` option will show you all information that `lpstat` is capable of displaying.

To illustrate how `lpadmin` is used, look at the following example. We're going to create a printer named `asimov`, which is an HP LaserJet 4 connected to the local parallel port, and make it part of the class named `lasers`. Then just for the purpose of illustration, we'll delete the printer.

![](bbox=[0.13, 0.71, 0.22, 0.78])

> NOTE
> Due to the size of the printed page of this edition, line lengths shown in the following code listing may not match your printout. Where overlong lines break onto another line, they have been indented three spaces.

```
[root@scribe root]# `lpinfo` -m |`grep` -i 'LaserJet 6P'   
   foomatic/HP/HP-LaserJet_6P-gimp-print-cups.ppd.gz HP LaserJet 6P,   
   Foomatic + gimp-print   
   foomatic/HP/HP-LaserJet_6P-gimp-print-ijs-cups.ppd.gz HP LaserJet 6P,   
   Foomatic + gimp-print-ijs
```