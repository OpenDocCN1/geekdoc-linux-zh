```
log_archive_dest_state_1 = enable  
log_archive_dest_state_2 = defer  
log_archive_dest_state_3 = enable
```

Using these parameters, ARC0 would copy the contents of the Redo Logs to two locations: /u01/oradata/PROD and /u03/oradata/PROD. Although the location /u02/oradata/PROD is configured as an archive location, it would not be used until its status is changed from DEFER to ENABLE. Changing a location’s status from DEFER to ENABLE can be accomplished by either editing the init.ora, or by issuing the ALTER SYSTEM SET LOG_ARCHIVE_DEST_STATE_n = ENABLE command.

![](bbox=[0.18, 0.36, 0.27, 0.44])

The dynamic data dictionary views VSARCHIVE_DEST and VSARCHIVED_LOG can be used to monitor the location and status of the archive activity in each archive destination.

![](bbox=[0.18, 0.49, 0.27, 0.57])

You can further reduce the likelihood that the Archiver process will create a bottleneck by specifying a device with fast I/O capabilities for the location for your archived Redo Log files.

![](bbox=[0.18, 0.61, 0.27, 0.69])

Raw devices cannot be used to store archive logs.

# Create Additional ARC0 Processes

LGWR implicitly starts additional Archiver processes any time the number of processes is inadequate to meet the instance’s archiving needs. However, you may want to experiment with explicitly starting additional Archiver processes if ARC0 appears to be causing a performance bottleneck. Additional Archiver processes are started by using the LOG_ARCHIVE_MAX_PROCESSES parameter in the init.ora. The number of Archiver processes to start is somewhat dependent upon the number of archive destinations you have specified and the speed of the devices that are behind those locations. The default value for this parameter is 1. The valid values for this parameter are from 1 to 10. These Archive processes will start immediately at instance startup.