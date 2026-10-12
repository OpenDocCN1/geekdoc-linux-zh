```
# If the config file attribute smart_user is defined as a string
# such as "$user@domain-gateway" then users not matched o
# therwise will be sent off to the host 'domain-gateway'.
#
# If the smart_user attribute is not defined, this director is
# ignored.
smart_user:
driver = smartuser;      # special-case driver

# do not match addresses which cannot be made into valid
# RFC822 local addresses without the use of double quotes.
well_formed_only
```

# Router Files

The router files differ slightly between workstations and a mail hub.

Since smail assumes uucp transport by default, these router files just force everything to be SMTP over an IP link. The two files differ only in that the workstation config uses the smarthost route, but the hub expects to be able to connect to the real destinations of messages.

# Workstation Routers File

```
# inet_addrs - match domain literals containing literal IP
# addresses. The library routine gethostbyaddr(3N) will be
# called to see if a reverse mapping to the cononical hostname
# is available.
inet_addrs:
driver = gethostbyaddr,    # router to match IP domain
# literals
transport = smtp;          # deliver using SMTP over
# TCP/IP

fail_if_error,             # fail malformed domain
# literal addrs
check_for_local            # see if this is really the
# local host

# paths - force some routes using the YP network path database
paths:  driver = pathalias,    # general-use paths router
transport = smtp;             # for matches, deliver over
# SMTP
```