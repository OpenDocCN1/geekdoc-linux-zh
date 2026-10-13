This session can be analyzed as follows:

+   - On lines 6-23 the faxsetup program issues warnings about not finding the vgetty, and egetty programs. These warnings can be safely ignored.
+   - On line 24 faxsetup indicates that a soft link needs to be created from `/var/spool/fax/bin/ps2fax` pointing to `/var/spool/fax/bin/ps2fax.gs`. Linux systems use ghostscript as the imaging engine, instead of the other default program. The RPM installation takes care of this and it can be safely ignored, unless you have compiled and installed HylaFAX from source.
+   - On lines 25-27 the fax user is created. HylaFAX runs its daemons as this user. However when you later check the processes with ps you will discover that HylaFAX daemons are running as the user uucp. This is fine, HylaFAX creates the fax user with the same UID as uucp.
+   - On lines 28 and 29 faxsetup informs you of the filenames where it has written the modem support functions and configuration parameters. This is useful information if you later need to tweak any of the values in these files.
+   - On lines 31-34 you provide faxsetup with the country code, area code, and local telephone number for the fax modem.
+   - On line 45 you get the chance to change the maximum number of pages for an outbound fax job.
+   - On line 54 faxsetup informs you where it saved the new configuration file.
+   - On lines 55-58 the HylaFAX daemons, hfaxd and faxq, are started up by running the script `/etc/rc.d/init.d/hylafax`. You are also informed that the daemons do not support the older fax protocol, or SNPP. If you need to support older fax clients or pagers, you must recompile from source code enabling these options.
+   - On lines 61 and 62 you are prompted to run the faxaddmodem program. This program queries the serial port where a fax modem is connected and then proceeds to configure it for use by HylaFAX.
+   - On lines 71-98 the modem connected to the serial port specified on line 62 is configured.
+   - On lines 99-120 the current configuration is displayed. On line 121 you are prompted to accept the configuration or make changes.
+   - On lines 122-149 faxsetup runs the probemodem program and tries to learn all its capabilities. The output of this section is modem specific and may not match your faxsetup output.
+   - On line 150 you are prompted to accept the modem configuration parameters. On acceptance the configuration is written and you are informed of its location.
+   - On line 151 a FIFO buffer is created for use by HylaFAX.
+   - On line 164 and 165 the configuration file is saved and any older configuration file from a previous run is backed up.