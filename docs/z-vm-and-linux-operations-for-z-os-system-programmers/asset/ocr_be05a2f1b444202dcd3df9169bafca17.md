# z/VM ONLINE

![](bbox=[0.15, 0.12, 0.85, 0.35])

built on IBM Virtualization Technology

Fill in your USERID and PASSWORD and press ENTER

> (Your password will not appear when you type it)

```
USERID ===>
PASSWORD ===>
COMMAND ===>
```

RUNNING VMLINUX6

# Figure 2-13 Logging on using the command line

The system prompts you for the password (see Example 2-3).

# Example-3 Prompt for the password

```
LOGON MAINT
```

```
ENTER PASSWORD (IT WILL NOT APPEAR WHEN TYPED):
```

After logging on, the CP READ prompt appears. Press Enter again and the CP loads CMS. See Figure 2-14 on page 56.

CMS then executes the PROFILE EXEC file of the z/VM user ID, if it exists. In the PROFILE EXEC, you can define settings for your z/VM user ID. For example, settings can be defined for PF window keys, linking to MDISKs, or loading (IPL) a guest operating system such as Linux or z/OS.