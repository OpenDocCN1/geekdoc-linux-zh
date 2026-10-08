different kinds of information that HAL manages, such as **policy**, whose subdirectories
have files with policies for how to manage devices. The files, known as device information
files, have rules for obtaining information about devices, as well as detecting and assigning
options for removable devices. The device information files have the extension **.fdi**, as in
*storage-methods.fdi*. For example, the **policy** directory has two subdirectories: **10osvendor**
and **20thirdpary**. The *10osvendor* holds the *.fdi* files that have policy rules for managing
removable devices on Fedora (*10osvendor* replaces *90defaultpolicy* in Fedora 3). This
directory holds the **20-storage-methods.fdi** policy file used for storage devices. Here you
will find the properties that specify options for removable storage devices such as CD-ROMs.
The directories begin with numbers; lower numbers are read first. Unlike with *udev*, the last
property read will override any previous property settings, so priority is given to higher-
numbered directories and the *.fdi* files they hold. This is why the default policies are in
*10osvendor*, whereas the user policies, which would override the defaults, would be in a
higher-numbered directory like *30user*, as are third-party policies, *20thirdpolicy*.

There are currently three device information file directories set up in the device information
file directories, each for different kinds of information: *information*, *policy*, and *preprobe*.

+   - **Information**  The *information* directory is for information about devices.
- **Policy**  The *policy* directory is for setting policies such as storage policies. The
default policies for a storage device are in a *20-storage-methods.fdi* file in the
*policy/10osvendor* directory.
- **Preprobe**  The *preprobe* directory handles difficult devices such as unusual drives
or drive configurations, for instance, those in *preprobe/10osvendor/10-ide-drives*
*.fdi*. This contains information needed even before the device is probed.

Within these subdirectories are still other subdirectories indicating where the device
information files come from, such as *vendor*, *thirdparty*, or *user*, and their priority. Certain
critical files are listed here:

+   - *information/10freedesktop*  Information provided by freedesktop.org
- *policy/10osvendor*  Default policies (set by system administrator and OS
distribution)
- *preprobe/10usevendor*  Preprobe policies for difficult devices

# Properties

Information for a device is specified with a *property* entry. Such entries consist of a key /
value pair, where the key specifies the device and its attribute and the value is the value for
that attribute. There are many kinds of values, such as Boolean *true*/*false*, string values
such as those use to specify directory mountpoints, or integer values.

Properties are classified according to metadata, physical connection, function, and
policies. Metadata provides general information about a device, such as the bus it uses, its
driver, or its HAL ID. Metadata properties begin with the key *info*, as in *info.bus*. Physical
properties describe physical connections, namely the buses used. The *IDE*, *PCI*, and *SCSI*
bus information is listed in *ide*, *pci*, and *scsi* keys. The *usb_device* properties are used for
the USB bus; an example is *usb_device.number*.

The functional properties apply to specific kinds of devices. Here you will find
properties for storage devices, such as the *storage.cdrom* keys that specify if an optical