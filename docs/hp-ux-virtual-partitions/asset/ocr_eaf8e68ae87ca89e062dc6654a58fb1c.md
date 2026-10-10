All applications in a vPar require startup scripts to be run as they would on any system (please see the non-vPar-specific section of this chapter if you need information on how HP-UX startup and shutdown operates.)

In the vPar used in this example we have a variety of applications running, including Broadvision. Let's take a look at *etc/rc.config.d*, where the configuration variable scripts are located, to see what *bv* files (those that relate to Broadvision) exist:

```
```
# ll | grep bv
-rwxr-xr-x    1 root        sys          9 Sep 26 09:31 bv
# cat bv
BV_CTL=1
#
```
```

This listing shows the *bv* file and its contents. The *BV_CTL=1* variable indicates that Broadvision is to be started when the system boots.

Starting the *bv* application processes results in several Broadvision-related daemons being started, including those shown in the following listing:

```
```
# ps -ef | grep bv1
pbcosmb    3111    3096   0 Sep 26 ?        0:04 bvcont_srv_p_1221_3 -f -install_name bv1tol/bvcont_srv...
 pbcosv    3404    3096   0 Sep 26 7        1:19 cntcdb_p_1221_5 -install_name bv1tol/cntcdb_1
pbcosbv   3707    3096   0 Sep 26 7        0:20 genericdb_p_1221_6 -install_name bv1tol/genericdb_1
pbcosbv   3479    3096   0 Sep 26 7:05 cntdb_p_1221_7 -install_name bv1tol
DiscussionForus_cntdb_1
root        7572    7232   0 13:17:33 pts/0                0:00 grep bv1
#
```
```

You can see that there are many processes related to the *bv1* application running on this system. These are started automatically as part of the startup structure of HP-UX. The following listing shows the link in */sbin/rc1.d*, for run level one, and */sbin/rc2.d*, for run level two, for *bv*.

```
```
# ll /sbin/rc1.d | grep bv
lrwxr-xr-x    1 root        sys          15 Sep 26 10:42 F10sbv -> /sbin/init.d/bv
# ll /sbin/rc2.d | grep bv
lrwxr-xr-x    1 root        sys          15 Sep 26 10:41 S930bv -> /sbin/init.d/bv
#
```
```