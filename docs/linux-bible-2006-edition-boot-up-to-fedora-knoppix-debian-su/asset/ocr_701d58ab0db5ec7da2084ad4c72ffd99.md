# Setting User Defaults

The useradd command determines the default values for new accounts by reading the /etc/login.defs file. You can modify these defaults by editing file manually with a standard text editor or by running the useradd command with the -D option. login.defs is different on different Linux systems, here is an example containing many of the settings you might find in a login.defs file:

```
PASS_MAX_DAYS   99999
PASS_MIN_DAYS  0
PASS_MIN_LEN   5
PASS_WARN_AGE   7

UID_MIN         500
UID_MAX         60000
GID_MIN         500
GID_MAX         60000
```

```
CREATE_HOME    yes
```

All uncommented lines contain keyword/value pairs. For example, the PASS_MIN_LEN is followed by white space and the value 5. This tells useradd that the user password must be at least five characters. Other lines let you customize the valid range of automatically assigned UID numbers or group ID numbers. (Red start at UID 500; other Linux start with UID 100.) A comment section that explains keyword's purpose precedes each keyword (which I edited out to save space). Altering a default value is as simple as editing the value with a keyword and then saving the file.

If you want to view the defaults, type the useradd command with the -D option, as follows:

```
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=-
SHELL=/bin/bash
SKEL=/etc/skel
```

You can also use the -D option to change defaults. When run with this flag, useradd refrains from actually creating a new user account; instead, it saves additionally supplied options as the new default values in /etc/login.defs. Not all useradd options can be used in conjunction with the -D option. You can use only the few options listed in Table 4-3.