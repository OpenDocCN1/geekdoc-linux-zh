# USING chfn

The chfn command runs an interactive process that enables you to set some personal information for your account. Run chfn on a command line without any options, as follows:

```
```
>chfn

Changing finger information for jray.
Password: *****
Name [John Ray]: John Ray
Office []: 7879 Rhapsody Drive
Office Phone []: (614) XXX-XXXX
Home Phone []: (614) XXX-XXXX
```
```

jray can change or set his full name, his office address, and his home and office phone numbers. If you're using chfn and you don't want to set a value, don't—you aren't forced to supply any of this information unless it is the policy of your company. Now that jray has added some information about himself, you can re-run the finger command to see the results.

Type the following:

```
```
>finger jray@poisontooth.com

[poisontooth.com]
Login: jray              Name: John Ray
Directory: /home/jray    Shell: /bin/bash
Office: 7879 Rhapsody Drive    Office Phone: (614) XXX-XXXX
Home Phone: (614) XXX-XXXX
On since Sun Nov 29 16:35 (EST) on tty0 from 192.168.0.91
6 hours 48 minutes idle
On since Sun Nov 29 21:47 (EST) on tty1 from 192.168.0.211
No mail.
No Plan.
```
```

That's a bit better! Now the office address and office/home phone numbers are shown correctly. Depending on how you use your system, you might not want to set any of this information. If that's the case, you can feel free to wipe the chfn command from your memory.