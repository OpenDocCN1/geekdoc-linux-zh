```
; guest ok = yes

# NOTE: If you have a BSD-style print system there
# is no need to specifically define each
# individual printer
[printers]
 comment = All Printers
 path = /var/spool/samba
 browseable = no
# Set public = yes to allow user 'guest account'
# to print
 guest ok = no
 writable = no
 printable = yes

# This one is useful for people to share files
;[tmp]
; comment = Temporary file space
; path = /tmp
; read only = no
; public = yes

# A publicly accessible directory, but read only,
# except for people in the "staff" group
;[public]
; comment = Public Stuff
; path = /home/samba
; public = yes
; writable = yes
; printable = no
; write list = @staff

# Other examples.
```