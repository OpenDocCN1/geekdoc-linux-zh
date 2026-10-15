# Printing with lp

If your Unix system is hooked up to a printer that you can access, you can print easily using the lp utility (Code Listing 15.6). (lp stands for line printer...you know, from the dark ages, practically.) If printing with lp is not a cinch, you likely have a system issue that you should address with the system administrator.



+   lp filename
+   At the shell prompt, type lp followed by the name of the file to print. Usually, you'll see confirmation that the file went to the printer, as shown in Code Listing 15.6.

+   lp -d otherprintername filename
+   You might, depending on your environment, want to specify a printer name. You do that by adding a -d (for destination) flag, as shown here.

```
Code Listing 15.6 Use the lp utility to print your files, rhymes, and more.
```

```
```bash
[jdoe@frazz jdoe]$ lp -d hplaser
request id is lp-46 (1 file(s))
[jdoe@frazz jdoe]$ lp -d hplaser
- limerick.rot13
request id is hplaser-85 (1 file(s))
[jdoe@frazz jdoe]$
```
```



+   Refer back to Chapter 6 for some text-formatting information. You can pipe data to lp, as in fmt ugly | pr | lp to format your document, add headers and footers, and print all at once.

+   Use lprq to get information about the printer queue. lprq will usually just respond that it's ready, but if you catch it at the right moment (or a lot of people are printing), it'll tell you which jobs are queued for printing.