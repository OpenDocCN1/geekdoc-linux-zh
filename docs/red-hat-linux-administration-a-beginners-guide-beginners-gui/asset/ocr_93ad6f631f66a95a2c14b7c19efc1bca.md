$(YPPWDDIR)

or

$(YPSRCDIR)

which are variables set up right before this section in the makefile. The default value for these variables is **/etc, **which means any occurrence of $(YPSRCDIR) will be replaced with /etc when the makefile is run. This allows you to point to where the files you want to share are located. **YPPWDDIR is a separate variable, just in case the password-related entries you want to share are separate from your real system files on the server. (Do you really want all the users on your system to have a login on the NIS server?) By default, your real files in /etc are pointed to, thus GROUP will become equal to /etc/group, PASSWD will become /etc/passwd, and so forth.

```
# These are the files from which the NIS databases are built. You
# may edit these to taste in the event that you want to keep your NIS
# source files separate from your NIS server's actual configuration
# files.
#
  GROUP         = $(YPPWDDIR)/group
  PASSWD        = $(YPPWDDIR)/passwd
  SHADOW        = $(YPPWDDIR)/shadow
  GSHADOW       = $(YPPWDDIR)/gshadow
  ADJUNCT       = $(YPPWDDIR)/passwd.adjunct
  ALIASES       = $(YPSRCDIR)/aliases		# could be in /etc or /etc/mail
  ALIASES       = /etc/aliases
  ETHERS        = $(YPSRCDIR)/ethers		# ethernet addresses (for rarpd)
  BOOTPARAMS    = $(YPSRCDIR)/bootparams # for booting Sun boxes (bootparamd)
  HOSTS         = $(YPSRCDIR)/hosts
  NETWORKS      = $(YPSRCDIR)/networks
  PRINTCAP      = $(YPSRCDIR)/printcap
  PROTOCOLCOLS  = $(YPSRCDIR)/protocols
  PUBLICKEYS    = $(YPSRCDIR)/publickey
  RPC           = $(YPSRCDIR)/rpc
  SERVICES      = $(YPSRCDIR)/services
  NETGROUP      = $(YPSRCDIR)/netgroup
  NETID         = $(YPSRCDIR)/netid
  AMD_HOME      = $(YPSRCDIR)/amd.home
  AUTO_MASTER   = $(YPSRCDIR)/auto.master
  AUTO_HOME     = $(YPSRCDIR)/auto.home
  AUTO_LOCAL    = $(YPSRCDIR)/auto.local
  TIMEZONE      = $(YPSRCDIR)/timezone
  LOCALE        = $(YPSRCDIR)/locale
  NETMASKS      = $(YPSRCDIR)/netmasks
```