# OffSec

functionality reinventing the wheel. Windows uses DLLs to store functionality needed by several components. Otherwise, each component would need the functionality in their source code resulting in a huge resource waste. On Unix systems, these files are Shared Objects.798

There are several methods we can use to exploit how DLLs work on Windows and they often be an effective method of elevating our privileges. One method is the privilege escalation vector in the previous section. By overwriting the binary, we merely overwrite a DLL the service uses. However, the service may not work as expected because the actual DLL functionality is missing. In most cases, this would still lead us to code execution of the DLL's code and, for example, to the creation of a new administrative user.

Another method is to hijack the DLL search order.799 The search order is defined by Microsoft and determines what is first when searching for DLLs. By default, all current Windows versions have safe DLL mode enabled.

This setting was implemented by Microsoft due to the high number of DLL hijacking vectors and ensures DLLs are more difficult to hijack. The following listing shows the standard search order taken from the Microsoft Documentation.800

+   1. The directory from which application is loaded.
2. The system directory.
3. The 16-bit system directory.
4. The Windows directory.
5. The current directory.
6. The directories that are listed in the PATH environment.

Listing 427 - Standard DLL search order on current Windows versions

Windows searches the application's directory. Interestingly, the current directory is at position S. When safe DLL search mode is disabled, the current directory is searched at position 2 after the application's directory.

A special case of this method is a missing DLL. This binary attempted to load a DLL that doesn't exist on the system. This often occurs with flawed installation processes or after updates. However, with a missing DLL, the program may still work with restricted functionality.

To exploit this situation, we can try placing a malicious DLL (with the name of the missing DLL) in a path of the DLL search order so when the binary is started.

Let's show how we can abuse a missing DLL in example by CLIENTWK220 over RDP and pass security/sNotAnOption++++. We will start PowerShell and enumerate the services as we did in the specified section. One finding is skipped the BetaServer.

```
PS C:\Users\steve> Get-Instance -ClassName win32_service | Select Name,State,PathName | Where-Object {$.State -like 'Running'}
```

| | State | PathName |

> 798 (Oracle Documentation, 2022), https://docs.oracle.com/cd/db/E19120-0/open-aris/819-0690/6n3zn7f8u/index.html

> 799 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/32/dlls/dynamic-library-framework-search-order

> 800 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/32/dlls/dynamic-library-framework-search-order

PWK - © 2023 OffSec Services Limited. All rights reserved.

508