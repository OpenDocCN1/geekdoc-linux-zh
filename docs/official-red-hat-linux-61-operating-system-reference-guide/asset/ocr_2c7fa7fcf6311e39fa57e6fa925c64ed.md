Currently, the correct values are:

+   - UTC=boolean, where boolean is the following:
+     - true -- indicates that the clock is set to UTC. Any other value indicates that it is set to local time.
+   - ARC=boolean, where boolean is the following:
+     - true -- (for Alpha-based systems only) Indicates the ARC console's 42-year time offset is in effect. Any other value indicates that the normal UNIX epoch is assumed.

+   - ZONE="filename" -- indicates the zonefile under /usr/share/zone-info that /etc/localtime is a copy of, for example:
+     ZONE="US/Eastern"

# /etc/sysconfig/hwconf

The /etc/sysconfig/hwconf file lists all the hardware that kudzu detected on your system, as well as the drivers used, vendor ID and device ID information. It is not meant to be edited. If you do edit it, devices could suddenly show up as being added or removed.

# /etc/sysconfig/mouse

The /etc/sysconfig/mouse file is used to specify information about the available mouse. The following values may be used:

+   - MOUSETYPE=type, where type is one of the following:
+     - microsoft -- A Microsoft mouse.
+     - mouseman -- A MouseMan mouse.
+     - mousesystems -- A Mouse Systems mouse.
+     - ps/2 -- A PS/2 mouse.
+     - msbm -- A Microsoft bus mouse.