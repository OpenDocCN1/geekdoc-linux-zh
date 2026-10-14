```
```
# cca_status -v -w memberUP,powerUP
Name       Type         R/RA   F/FT   Target   State    Host
memberUP   application  0/1    0/0    ONLINE   ONLINE   molari
powerUP    application  0/1    0/0    OFFLINE  OFFLINE
```
```

Should it have? No, powerUP is only “optional”, therefore, memberUP will not stop (or even relocate). If powerUP were “required” however...

+   2.

powerUP is a REQUIRED RESOURCE of memberUP.

The first thing we need to do here is modify memberUP’s profile, stop memberUP, and update the registry.

```
```
# cca_profile -updates memberUP -1 " -R powerUP"; cca_stop memberUP

Attempting to stop memberUP on member 'molari'
Stop of 'memberUP' on member 'molari' succeeded.
```
```

```
```
# cca_register -u memberUP / cca_start memberUP

Attempting to start 'powerUP' on member 'molari'
Start of 'powerUP' on member 'molari' succeeded.
Attempting to start 'memberUP' on member 'molari'
Start of 'memberUP' on member 'molari' succeeded.
```
```

Note that powerUP started as well. This is due to the fact that memberUP now requires powerUP to be running on the same member. Let’s see what happens if we attempt to relocate or stop powerUP.

```
```
# cca_relocate powerUP

sheridan : Resource memberUP (application) is running on molari

Resource powerUP has placement error.
```
```

```
```
# cca_stop powerUP

Resources depending on powerUP are running
Resource powerUP has placement error.
```
```

No joy. Can we force powerUP to relocate or stop? The “-f” option to the caa_relocate (or caa_start) command allows CAA to stop and/or start those resources, upon which the application resource depends, to enable the task to succeed. For example, since we want to relocate memberUP to molari, but memberUP requires powerUP (which is currently on sheridan), stop powerUP as well as memberUP and start them both on molari.