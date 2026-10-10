Organization: *Universal AeroSpace*                 Page 1 of 3
Developed by: *Eric Kenton*                         Date:
Container Context: *Engineering.UAS*

```
**REM General Commands**
REM Created by: Eric Kenton
REM Last modified: 12/15/2005
NO_DEFAULT
MAP DISPLAY OFF
CONTEXT        ..Engineering.UAS
MAP ROOT G:=UASHOST_CORP:\
MAP L:=EngData
MAP INS S1:=UASHOST_SYS:PUBLIC
CLS
WRITE "Good $GREETING_TIME, $LOGIN_NAME"
WRITE "Welcome to the Universal AeroSpace network system"
DISPLAY UASHOST_CORP:\Shared\Messages\$DAY_OF_WEEK.MSG
IF DAY_OF_WEEK<"Monday" and HOUR24 < "09" THEN BEGIN
    WRITE "Weekly design meeting at 9:00 a.m. in conference room"
END
PAUSE
```

```
**REM Commands for Design Workgroup**
IF MEMBER OF "Design" THEN
    MAP ROOT P:=L:CAD
END
```

```
**REM Commands for ITMgrs Workgroup**
IF MEMBER OF "ITMgrs" THEN BEGIN
    MAP P:=UASHOST_SYS:
END
```

```
**REM End of Login Script Commands**
```

**Figure 9-22**    The Engineering container login script

![](bbox=[0.94, 0.28, 0.98, 0.31])