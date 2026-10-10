```
echo.
echo     Q). What's the worst thing about being an egg?
echo     A). You only get laid once.
echo.
echo HAHAHAA, get it? Don't you just love that one?
echo.
:end
```

**Hack State:** Password theft.

**File:** ProgenicMail.zip.

**Synopsis:** Hackers use the ProgenicMail technique to dupe victims into sending all cached system passwords. The program operates in a simple fashion, better explained on a per-file basis:

+   - *Psetup.dat.* This file contains the custom configurations options:
+   
+   [Setup]
+   
+   Mail=(email address to forward passwords to)
+   
+   Data=ProgenicMail (if left blank, the program will send passwords upon each execution)

+   - *setup.dll.* This file can be replaced with any .exe to be loaded to hide the true purpose of the attack. For example, the attacker may rename a joke.exe as setup.dll. The program will then launch setup.dll (really joke.exe) as it forwards all system passwords to the attacker.

**Hack State:** Unrecoverable file deletion.

**File:** FFK.exe.

**Synopsis:** After penetrating a system, hackers will attempt to delete logs and trace back evidence with an unrecoverable file deletion utility. The purpose of this program, by PhrozeN, is to permanently delete files very fast. For example, with Fast File Killer (shown in Figure 10.14), 4,000 files of 3–150 KB take

![](bbox=[0.13, 0.62, 0.565, 0.939])