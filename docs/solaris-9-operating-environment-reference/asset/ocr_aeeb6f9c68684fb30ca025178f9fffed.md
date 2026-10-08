# kinit

# 563

after a specified lifetime, after which you must run kinit again to refresh the tickets. Any existing contents of the cache are destroyed by kinit. Use the kdestroy(1) command to destroy any active tickets before you end your login session.

# Configuration File

You must configure the system on which you plan to run kinit as a Kerberos client by making the appropriate modifications to the /etc/krb5/krb5.conf file. The default krb5.conf file is shown below.

```
#
#pragma ident "(@)krb5.conf 1.2 99/07/20 SMI"
# Copyright (c) 1999, by Sun Microsystems, Inc.
# All rights reserved.
#
#krb5.conf template
# In order to complete this configuration file
# you will need to replace the __name>__ placeholders
# with appropriate values for your network.
#
[libdefaults]
  default_realm = __default_realm__

[realms]
  default_realm = (
    kdc = master_kdc_
    _slave_kdc_
    admin_server = master_kdc_
  )

[domain_realm]
  domain_mapping_

[logging]
  default = FILE:/var/krb5/kdc.log
  kdc = FILE:/var/krb5/kdc.log
krotate = {
# How often to rotate kdc.log. Logs will get rotated more
# often than the period, and less often if the KDC is not used
# frequently.

  period = 1d

# how many versions of kdc.log to keep around (kdc.log.0, kdc.log.1, ...)

  versions = 10

[appdefaults]
  kinit = {
    renewable = true
```