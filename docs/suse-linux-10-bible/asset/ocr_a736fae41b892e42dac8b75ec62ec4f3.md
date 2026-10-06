# Chapter 12 + Working with Packages 337

# Listing 12-8: The %install Section for logcheck

```
%install
rm -rf $RPM_BUILD_ROOT/usr/sbin
mkdir -p $RPM_BUILD_ROOT/etc/logcheck
mkdir -p $RPM_BUILD_ROOT/etc/cron.hourly

install ... ./systems/linux/logcheck.hacking $RPM_BUILD_ROOT/etc/logcheck
install ... ./systems/linux/logcheck.violations $RPM_BUILD_ROOT/etc/logcheck
install ... ./systems/linux/logcheck.violations.ignore $RPM_BUILD_ROOT/etc/logcheck
install ... ./systems/linux/logcheck.ignore $RPM_BUILD_ROOT/etc/logcheck
install ... ./systems/linux/logcheck.sh $RPM_BUILD_ROOT/usr/sbin
install ... ./src/logcheck $RPM_BUILD_ROOT/usr/sbin

cat <<EOF > $RPM_BUILD_ROOT/etc/cron.hourly.logcheck
!/bin/sh
exec /usr/sbin/logcheck.sh
EOF
```

The %install macro is the most involved section because you have to it pre-pare the RPM_BUILD_ROOT for RPM packaging.

+   1. First, you need to make sure you have a fresh RPM build in case a previous build take place and did not complete successfully. This is done with the rm -rf $RPM_BUILD_ROOT directive.

+   2. Next, you need to create the target directories for the installed files. In this example, the logcheck binaries are located in /usr/sbin and the configuration files are located in /etc/logcheck.

> The RPM_BUILD_ROOT is an effective root. This means it is a representation of where files would be located after the RPM has been installed in the root (/) directory.

+   3. The install process is effectively the same as cp. It copies a file from one location to another. Here you are copying files to the location they would be in an installed system, RPM_BUILD_ROOT.

+   4. The cat entry is a nice way of creating a file out of using redirection. The redirection will enter the text following the cat program until EOF (end of file) is found. This will create an entry in /etc/cron.hourly for logcheck to run once an hour.