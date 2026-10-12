configuration files), which allows aliases to be created for accounts that are no longer active. For example, if the `/etc/aliases` file contained the following line:

```
jeff: jeff@newplace.com.REDIRECT
```

Any mail sent to jeff on the local machine would result in an informational message being returned to the original sender, indicating the changed address. The original mail message will not be forwarded to the address listed in the jeff example above. The DZ8.11.4 line sets the macro Z, which contains the full version information for the sendmail daemon.

# ## sendmail options

The sendmail.cf file contains a long list of options that you can set for sendmail on your Red Hat Linux system. Option definitions start after the Options block. Here is an example of the beginning of the Options section:

```
##################
#   Options   #
##################

# strip message body to 7 bits on input?
O SevenBitInput=False

# 8-bit data handling
# O EightBitMode=pass8
```

The SevenBitInput option indicates that sendmail should not clear the most significant bit from each byte of all mail messages. The EightBitMode dictates how sendmail should handle message data that is not explicitly labeled as 8-bit. The pass8 option allows any 8-bit data to be delivered unaltered; mimefy converts any unspecified data to a MIME-encoded type; strict rejects any unlabeled 8-bit data. Note that this option has no effect on data that is specified as 8-bit. The next lines relate to alias files:

```
# wait for alias file rebuild (default units: minutes)
O AliasWait=10

# location of alias file
O AliasFile=/etc/aliases
```

Before rebuilding the aliases database, sendmail performs several checks to make sure that no other processes are attempting to do the same. The AliasWait option specifies the number of minutes that sendmail alternates between waiting and performing its checks. The AliasFile option specifies the location of the plain-text file containing mail aliases. The next lines relate to how disk space is allocated for sendmail:

```
# minimum number of free blocks on filesystem
O MinFreeBlocks=100

# maximum message size
```