# **Table 16.9** **Win32::NetAdmin Extensions**

Win32::NetAdmin::UserGetAttributes( $Machine,
$UserName,
$Password,
$PasswordAge,
$Privilege,
$Homedir,
$Comment,
$Flags,
$ScriptPath);

Win32::NetAdmin::UserSetAttributes ( $Machine,
$UserName,
$Password,
$PasswordAge,
$Privilege,
$Homedir,
$Comment,
$Flags,
$ScriptPath);

# **EXAMPLE 16.39**

```
1 use Win32::NetAdmin qw(GetUsers UserGetAttributes);
2 GetUsers('*', FILTER_NORMAL_ACCOUNT) or die;
3 foreach $key (sort keys %hash) {
    print "$key\n";
}

(Output)
Administrator
Elise Quigley
Guest
```

You cannot transfer encrypted passwords from UNIX to Win32 systems, and vice versa. They are cryptographically incompatible. To manage passwords, use the Win32::AdminMisc or the Win32::NetAdmin module extension. See Table 16.10.