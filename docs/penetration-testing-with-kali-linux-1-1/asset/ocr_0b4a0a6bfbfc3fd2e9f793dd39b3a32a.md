![](bbox=[0.12, 0.03, 0.27, 0.08])



```
WWAN AutoConfig                WwanSvc
C:\Windows\system32\svchost.exe -k LocalServiceNoNetwork

Manual
```

*Listing 966 - Getting services via wmic*

This is great information but there is way too much of it for us to review manually. We will narrow it down to services that are automatically started by piping the `wmic` command to `findstr` to look for the word “auto”. We also include the `/i` flag to make the search case insensitive.

```
C:\Users\alex>wmic service get name,displayName,pathname,startmode | findstr /i "auto"
Application  Identity    AppIDSvc
C:\Windows\system32\svchost.exe -k LocalServiceAndNoImpersonation

...
WWAN AutoConfig                 WwanSvc
C:\Windows\system32\svchost.exe -k LocalServiceNoNetwork

Manual
```

*Listing 967 - Getting services via wmic that are automatically started*

This output is better, but it’s not ideal. We can still take out services that are started from the `c:\windows` folder to get a list of non-standard services. This can be done by piping the command we have so far into `findstr` again and using the `/v` flag to ignore anything that contains the string “c:\windows”.

```
C:\Users\alex>wmic service get name,displayName,pathname,startmode | findstr /i "auto"
| findstr /i /v "c:\windows"
McAfee Agent Common Services    macmsnsvc
"C:\Program Files\McAfee\Agent\macmsnsvc.exe" /ServiceStart

McAfee Agent Service          Auto masvc
"C:\Program Files\McAfee\Agent\masvc.exe" /ServiceStart

McAfee Service Controller     Auto mfmms
"C:\Program Files\Common Files\McAfee\SystemCore\mfemms.exe"

McAfee Endpoint Security Web Control Service  Auto mfewc
"C:\Program Files (x86)\McAfee\Endpoint Security\Web Control\mfewc.exe"

Puppet Agent                  Auto puppet
C:\Puppet\Current Version\sys\ruby\bin\ruby.exe --rubygems "C:\Puppet\Current Version\service\daemon.rb"
```