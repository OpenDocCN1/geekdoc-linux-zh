The post field contains the list of who has permission to post this event class.

The access field contains the list of who has permission to retrieve or subscribe to this class of event.

The rights_list is defined in Table 8-6.

The rights_list must be enclosed in double-quotes (" ") if it contains spaces. Multiple users and/or groups in the rights_list must be separated by a comma (,). The root user has implicit rights to all events and services unless explicitly denied.

For example:

```
event_rights {
        class  @SYS_VP@.binlog     # binary error log events
        post   root
        access "root, group=adm"
}
```

The root user can post events of type ‘sys.unix.binlog’, and the root user and users in the adm group can retrieve the events. If you are concerned about future portability, you should use the @SYS_VP@ macro to refer to system (sys.unix) events.

+   - `service_rights`

This entry type defines the rights for a particular service to be performed by the daemon for a requesting client. Each service_rights entry contains two fields:

```
service_rights {
        service  service_name
        execute  rights_list
}
```

The service field contains the particular service. Services must be defined in /etc/evmdemon.conf. User-defined services are not supported as of this writing.

![](bbox=[0.263, 0.716, 0.735, 0.906])

# Table 8-6: Event Authorization Rights