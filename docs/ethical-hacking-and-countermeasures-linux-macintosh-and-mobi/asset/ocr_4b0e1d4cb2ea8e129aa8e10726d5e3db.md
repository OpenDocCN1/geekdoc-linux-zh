+   HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\avp.  exe"Debugger" = <System>\drivers\pnpifj.exe

+   HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\iparmo.  exe"Debugger" = <System>\drivers\pnpifj.exe

+   HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\kabaload.  exe"Debugger" = <System>\drivers\pnpifj.exe

+   HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\mmsk.  exe"Debugger" = <System>\drivers\pnpifj.exe

+   HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\msconfig.  com"Debugger" = <System>\drivers\pnpifj.exe

+   HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\msconfig.  exe"Debugger" = <System>\drivers\pnpifj.exe

+   HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\regedit.  com"Debugger" = <System>\drivers\pnpifj.exe

+   HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\regedit.  exe"Debugger" = <System>\drivers\pnpifj.exe

+   HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\runiep.  exe"Debugger" = <System>\drivers\pnpifj.exe

+   HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon"Shell" = Explorer.exe <Sys-  tem>\drivers\conime.exe

# Worm: W32/VBAt-B

The W32/VBAt-B worm affects the Windows platform. This worm spreads through instant messaging proto-  cols and removable storage devices, and it downloads, installs, and runs new software. The worm attempts to  copy itself with the file boot.exe to the available removable storage device. It then creates Autorun.inf to ensure  that the worm is executed when the device is accessed. Autorun.inf can be safely deleted.

The worm copies itself to the following files when it is run for the first time:

+   <Windows>\lsass.exe

+   <System>\lsass.exe

The following registry entries are changed to run lsass.exe on startup:

+   HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon"Shell" = explorer.exe  <System>\lsass.exe

+   HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon"Userinit" = userinit.  exe,<System>\lsass.exe

Internet Explorer settings are changed by modifying values under the following registry entry:

HKCU\Software\Microsoft\Internet Explorer\Main\Start Page

System software is disabled by setting the following registry entries:

+   HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\System"DisableRegistryTools" = 1

+   HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\System"DisableTaskMgr" = 1

+   HKLM\SOFTWARE\Policies\Microsoft\Windows NT\SystemRestore"DisableConfig" = 1

The worm also sets the following registry entries:

+   HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer"NoFolderOptions" = 1

+   HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer"NoRun" = 1

+   HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer"NoFolderOptions" = 1

+   HKCU\Software\Policies\Microsoft\Internet Control Panel"Homepage" = 1

+   HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced"Hidden" = 2

+   HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\HideFileExt" = 1