# Listing 7.7 ABEL code generated for the CNT3SE state machine. (Cont’d.)

```
042-    OUTPUT='b00;
043-    IF (!RESET&!UP) THEN
044-        S2
045-    ELSE IF (!RESET) THEN
046-        S0
047-    ELSE IF (!RESET&UP) THEN
048-        S1;
049-
050-    State S1:
051-
052-    OUTPUT='b01;
053-    IF (!RESET&UP#!RESET) THEN
054-        S0
055-    ELSE IF (!RESET&UP) THEN
056-        S2;
057-
058-
059-    State S2:
060-
061-    OUTPUT='b10;
062-    IF (!RESET&UP#!RESET) THEN
063-        S0
064-    ELSE IF (!RESET&UP) THEN
065-        S1;
066-
067-
068-    " end of state machine - Sreg0
069-
070-    end cnt3se
071-
072-
```

A user-constraint file for the CNT3SE design should assign the inputs and outputs like this for the XS40 Board:

```
NET CLK      LOC=P44;  # B0 argument of XSPORT
NET RESET    LOC=P45;  # B1 argument of XSPORT
NET UP       LOC=P46;  # B2 argument of XSPORT
NET OUTPUT0  LOC=P25;  # S0 LED segment
NET OUTPUT1  LOC=P26;  # S1 LED segment
```

Or use the following constraints for the XS95 Board: