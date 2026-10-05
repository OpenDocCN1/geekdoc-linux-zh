# OffSec

The simplest way to do this is to right-click the Notepad icon on the desktop then shift-left click "show more options" on the popup, yielding the options in Figure 285.

![](bbox=[0.301, 0.147, 0.698, 0.701])

Figure 285: Enabling extra options

From here, we enter jen as the username with the associated password, which will launch Notepad in the context of that user. After successful authentication, jen's credentials will be cached on this machine.

We can validate this with the securisa:logonpasswords command from mimikatz after spawning an Administrative shell. The command will dump the cached password hashes.

```
mimikatz # privilege::debug
Privilege '20' OK
mimikatz # securisa::logonpasswords
```