![](bbox=[0.09, 0.09, 0.34, 0.18])

Save the file in your scripts directory, then open a Command Prompt window there and run this program – to see memory space handled by garbage collection

```
```text
Command Prompt
C:\MyScripts>python garbage.py
Koko Is Born...
Koko ID: 24243888
Koko Sings: Tweet, tweet!

Koko Flew Away!

Louie Is Born...
Louie ID: 24243888
Louie Sings: Chirp, chirp!

Misty Is Born...
Misty ID: 24244016
Misty Sings: Squawk, squawk!

Louie Flew Away!

Misty Flew Away!

C:\MyScripts>•
```
```

![](bbox=[0.11, 0.63, 0.22, 0.73])

The second instance created here is allocated the memory address vacated when the first instance was deleted.