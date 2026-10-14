specified user ID. The effective user ID is the user ID currently in effect for the process, although it may not be the user ID of the person logged in.

The format of the su command is:

```
su username
```

The *username* entry is the user name whose identity you want to assume.

If, after altering your identity, you want to confirm what identity you have assumed, use the whoami command. This command displays the user name of the identity you have assumed.

After completing your work under a new identity, you should return to your own login identity. To do so, press Ctrl/D or enter the exit command.

Example 5–3 shows how Juan assumes Lucy's identity, confirms it, removes a file, and then returns to his own login identity.

# Example 5–3: Using the su Command

```
$ whoami
juan
$ su lucy
Password: ...
$ whoami
lucy
$ rm file9
$ exit
$ whoami
juan
$
```

The following list items correspond to the numbers in the example:

+   1. Juan verifies his current identity with the whoami command.
+   2. Juan uses the su command to assume the identity lucy.
+   3. For security reasons, any display of the password is suppressed.
+   4. Juan verifies that he has assumed the identity lucy.
+   5. Juan removes a file.
+   6. Juan uses the exit command to return to his own identity.

For more information, see the su(1) and whoami(1) reference pages.

# 5.7 Superuser Concepts

Every system has a superuser who has permissions that supersede those of ordinary users. This superuser is often referred to as root.