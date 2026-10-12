Entries in `/etc/initab` use a field-based notation that determines the runlevel—when to execute the process, whether or not the process is executed when booting, whether or not to wait for the process to complete, and when to execute the process during booting. The default choices are adequate and need be changed only in unique circumstances that the average user is not likely to encounter.

The value of the default entry, or the `initdefault` line in `/etc/initab`, determines the particular system state that Fedora is in when the login prompt is finally presented. For example,

```
id:5:initdefault:
```

In this example, Fedora boots to runlevel 5, a network-enabled, multiuser mode with an active X session and a graphical login. The value 5 is forwarded to the script named `rc` under the `/etc/rc.d` directory. This script is used when booting or changing runlevels; it also acts as an interpreter when you boot Fedora in interactive mode by pressing **1** during the boot.

After `rc/rc.d/rc.sysinit` has finished, `init` uses the corresponding `/etc/initab` entry that matches the designated default runlevel. Using the previous example, the line in `/etc/initab` would then be

```
15:5:wait:/etc/rc.d/rc.5
```

Under the `/etc/rc.d` directory is a series of directories that correspond to each runlevel:

```
# ls /etc/rc.d
init.d  rc0.d  rc2.d  rc4.d  rc6.d  rc.sysinit
rc      rc1.d  rc3.d  rc5.d  rc.local
```

Assuming that the value is 5, the `rc` script executes all the scripts under the `/etc/rc.d/rc.5` directory and then launches the graphical login.

If Fedora is booted to runlevel 5, for example, scripts beginning with the letter K followed by scripts beginning with the letter S under the `/etc/rc.d/rc.5` directory are then executed:

```
# ls /etc/rc.d/rc5.d/
K01yum    K20bootparamd  K28amd    K45named  K61ldap
K74ypxfrd  S05kudzu     S24pcmcia  S85gpm    K05innnd
K201sccs1  K30sendmail   K46radvd   K651ident K84bgpd
S08ip6tables S25netfs   S90crond K05sslauncher K20netdump-server
K34ndcrelay K50netdump   K65kadmin  K84ospf6d   S08ipchains
S26apmd   S90freenvd  K10psacct  K20nfs    K34ypassswd
K50snmpd  K65kproo   K840spad   S08ipables  S28autofs
S90xfs   K10radius  K20rsstd   K35atalk   K50snmptrapd
K65krb524  K84ripd  S10network S40smartd S9211isa  S65krb5dc
K12canna K20usersd K35dhcpd K50tux
```