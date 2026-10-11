Table 6.2 Description of Important OPIE configuration Options

| OPIE configure Option | Description |
| :--- | :--- |
| --enable-user-locking=[DIR] | Allows for the specification of an alternate location for lock file directory. Default is /etc/opielocks. The purpose of these lock files is to mitigate race attacks and are implemented as required by RFC2289. |
| --disable-user-locking | Disables the use of lock files. |
| --enable-access-file=FILENAME | Enable the use of an access control list. FILENAME is replaced with the absolute pathname of the file. By default this option is disabled and is not recommended. |
| --enable-su-star-check | Causes all su attempts by users with no valid password (* in the password field) to fail. This does apply to root. Only meaningful if you use the replacement su program. |
| --enable-insecure-override | Ordinarily, OPIE will disallow the disclosure of the secret password over the network. Setting this configuration option allows the use of the -f flag with opie-passwd and opiekey to override the security checks. Use of this option is not recommended. |
| --enable-server-md4 | Causes the server-side applications to use MD4 instead of MD5. MD5 is the default and is recommended. |

# Example 6-18 Running configure for OPIE

```
# ./configure --enable-access-file=/etc/opieaccess
creating cache ./config.cache
Using the access file in /etc/opieaccess -- don't say we didn't warn you!
checking for gcc... gcc
checking whether the C compiler (gcc ) works... yes
checking whether the C compiler (gcc ) is a cross-compiler... no
checking whether we are using GNU C... yes
....
<lots of output snipped>
...
checking for nonstandard gettimeofday... no
updating cache ./config.cache
creating ./config.status
creating configure.munger
creating libmissing/Makefile
creating libopie/Makefile
creating Makefile.munge
creating config.h

Binaries are going to be installed into /usr/local/bin,
Manual pages are going to be installed into /usr/local/man.
creating Makefile

Have you read the README file?
#
```