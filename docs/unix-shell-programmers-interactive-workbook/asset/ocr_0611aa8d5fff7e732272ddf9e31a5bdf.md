# Lab 10.3: Parameter Expansion

which is printed after line 1047, whereas the := assigns the default value to the variable so that it can be used later on, as when its value is printed on line 1049.

# 10.3.2 ANSWERS

Run the following commands:

```
unset BROWSER
BROKER=
[[ $BROWSER == $BROKER ]] && print They are the same
```

+   a) Does the message print?
   Answer:Yes.

BROWSER is not set, but BROKER is set to the empty string. If you print them, you will get nothing in both cases. They appear to be indistinguishable.

+   b) Are the two variables really the same?
   Answer:No.

BROWSER has explicitly been unset, given no value. However, BROKER has been set, it's just that the value to the right of the equal sign is the empty string. The assignment to BROKER could also have been written as follows:

```
BROKER=" "
```

Run the following commands:

```
unset BROWSER
print ${BROWSER-lynx}
BROWSER=
print ${BROWSER-lynx}
BROWSER=netscape
print ${BROWSER-lynx}
```

+   c) Explain the outputs of the three print commands.
   Answer:Your interaction should look like the following:

```
[1050]: unset BROWSER
[1051]: print ${BROWSER-lynx}
lynx
```