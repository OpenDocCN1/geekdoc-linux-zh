Several programs and scripts that are used while processing the send and receive queues are placed in `/var/spool/fax/bin`:

+   - `mkcover`
+   - `notify`
+   - `notify.awk`
+   - `pcl2fax`
+   - `pollrcvd`
+   - `ps2fax`
+   - `ps2fax.dps`
+   - `ps2fax.gs`
+   - `ps2fax.imp`
+   - `tiff2fax`
+   - `wedged`

The etc directory under `/var/spool/fax` holds more configuration files, templates, and the fax transmission log file. These are as follows:

+   - `cover.templ`
+   - `dialrules`
+   - `dialrules.europe`
+   - `dialrules.sf-ba`
+   - `dpsprinter.ps`
+   - `hosts`
+   - `lutRS18.pcf`
+   - `xferfaxlog`

Plain text and html documentation are installed in `/usr/doc/hylafax-n.n.n`, where `n.n.n` is the software version number.

# ## CONFIGURING HYLAFAX SERVER

The term HylaFAX server is used to define a machine that has one or more fax modems installed on it and is capable of servicing fax requests both from itself and from networked client machines. Basically the server machine has the complete set of fax client and server software installed.

The faxsetup program must be run to configure HylaFAX before it can be used as a fax server. However it is necessary to have one or more properly functioning fax modems installed on the fax server before you run faxsetup.