Again, unless you have an especially complicated routing scheme on your NetWare network, there is probably no reason to change the value of the parameter for section 5.

Section 6 of the /etc/nwserv.conf file determines the version of NetWare that we will emulate. This section is shown in Listing 18.6.

# LISTING 18.6 Section 6 of the /etc/nwserv.conf File—Version Spoofing

```
# ==================================================
# Section 6: version-"spoofing"
#
# Some clients work better if the server tells that it is a 3.11 Server,
# although many calls (namespace services) of a real 3.11 Server are
# missing yet.
# To test the namespace calls, this entry must be set to > 0 and `config.h`
# must be altered before compiling "mars_nwe".
#
# ............................................................
#
# Syntax:
# 6 SERVER_VERSION
#
# SERVER_VERSION: the version-number reported to DOS-clients
# 0 Version 2.15 (default)
# 1 Version 3.11
# 2 Version 3.12 (not implemented yet)
# ............................................................
#
6 0
```

The value that you set in section 6 helps to define your capabilities to the client. The default value as shown in Listing 18.6 is the safest bet; however, if you follow the example in the IPX-HOWTO, you will set the value of this parameter to 1 for version 3.11.

The next section of the configuration file shown in Listing 18.7 sets the password handling policy. The syntax is the section number followed by a numeric flag that specifies how passwords will be handled for DOS clients. The comments in the listing explain the meaning of the possible numerical values.