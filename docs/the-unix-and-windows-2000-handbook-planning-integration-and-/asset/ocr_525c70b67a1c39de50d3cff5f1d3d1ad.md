# CHAPTER 16  Web Servers

The first command, configure, executed under APACL, is the most important. The command configure accepts approximately 40 options. To obtain a listing of all options that configure supports, execute the following command:

```
#configure --help
```

The following listing contains only the Configuration options: portion of the configure -1 command:

```
Configuration options:
--enable-rule=NAME        enable a particular Rule named 'NAME'
--disable-rule=NAME       disable a particular Rule named 'NAME'
                          [DEV_RANDOM=default EXPAT=default    IRIXN32=yes
                           [IRIXN32=no       PARANOID=no       SHARED_CHAIN=de]
                           [SHARED_CORE=default SOCKS4=no      SOCKS5=no     ]
                           [WANTSHAREDEXEC=default
--add-module=FILE         on-the-fly copy & activate a 3rd-party Module
--activate-module=FILE    on-the-fly activate existing 3rd-party Module
--permute-module=NAME     on-the-fly permute module 'NAME' with module 'N2'
--enable-module=NAME      enable a particular Module named 'NAME'
--disable-module=NAME     disable a particular Module named 'NAME'
                          [access=yes       actions=yes       alias=yes
                           asis=yes         auth_anon=no      auth_dbm=no
                           auth_db=no       auth_digest=no    auth=yes
                           autindex=yes     cern_meta=no      cgi=yes
                           digest=no        dir=yes           env=yes
                           example=no      expires=no        headers=no
                           imap=yes         include=yes       info=no
                           log_agent=no     log_config=yes    log_referer=no
                           mime_magic=no   mime=yes           mmap_static=no
                           negotiation=yes proxy=no          rewrite=no
                           setenvif=yes     so=no             spelling=no
                           status=yes       unique_id=no      userdir=yes
                           usertrack=no     vhost_alias=no   ]
--enable-shared=NAME      enable a build of Module named 'NAME' as a DSO
--disable-shared=NAME     disable build of Module named 'NAME' as a DSO
--with-perl=FILE          path to the optional Perl interpreter
--without-support         disable the build and installation of support tools
--without-confadjust      disable the user/situation adjustments in config
--without-execstrip       disable the stripping of executables on installation
```

Under the --disable-module=NAME heading is a listing of the standard modules included in the Apache Web Server distribution. Modules that are assigned a value of yes (access=yes, mime=yes...) are included by default. Modules assigned a value of no (mime_magic=no, so=no...) are not included by default. The modules mime_magic and rewrite will be added for this Web Server. Each module added will require a separate --enable-module (--enable-module=mime_magic) option on the configuration command line. We have also decided that the rewrite