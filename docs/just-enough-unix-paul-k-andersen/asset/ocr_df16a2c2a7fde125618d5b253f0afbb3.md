```
$ stty erase ^h Return
```

Note that the carat (^) is used to represent the Control key.

# A.3 Setting the Terminal Echo

As you type characters on the keyboard, the system is supposed to echo them back to you on the terminal screen (except when you are entering your password). If what you type does not appear on the screen, you can turn on the echo using the following command:

```
$ stty echo Return
```

On the other hand, if every character is being echoed twice, you should turn off the echo:

```
$ stty -echo Return
```