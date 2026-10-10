This chapter discusses a variety of hardware and software used with Linux during data input on your notebook. You'll learn about using Linux in text-only (*console*) mode, how to control your built-in or external mouse and keyboard, and how to use various X11 clients to make life easier when typing or browsing with the X Window System.

# # Linux Input Software

Linux comes with an incredible host of programs you can use to control your keyboard and mouse. You'll find support for a variety of pointing devices, keyboards, and languages. Some of this software is listed in Table 10.1.

Many of the programs listed in Table 10.1 are well-documented and come with man pages you can read with the man command.

# # Using Your Mouse with the Console

When you install and boot Linux, your notebook's built-in pointer should be recognized and configured automatically. You'll probably see something like this (on Intel-based notebooks):

```
```
.
Detected PS/2 Mouse Port.
.
```

```

Apple iBook users using Yellow Dog Linux will see a more cryptic statement:

```
```
...
adb devices: [2]: 2 c2 [3]: 3 1 [7]: 7 1f
...
Macintosh ADB mouse driver installed.
...
```

```

If you boot Linux to console (text-only) mode, the gpm mouse server provides services you need to use the mouse to point, click on dialog box buttons, drag to select, and copy and paste text. gpm is a complex piece of software with more than two dozen command-line options.