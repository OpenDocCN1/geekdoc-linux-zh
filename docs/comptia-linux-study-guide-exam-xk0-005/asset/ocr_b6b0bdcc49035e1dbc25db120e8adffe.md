In Listing 4.14, the password file is being audited for all accounts that use the /sbin/nologin shell via the grep command. The grep command’s output is lengthy and was snipped in the listing. It would be so much easier to redirect STDOUT to a file. This was done in Listing 4.14 by issuing the same grep command but tacking on a redirection operator, >, and a filename to the command’s end. The effect was to send the command’s output to the file NoLoginAccs.txt instead of the screen. Now the data file can be viewed using the less utility.

![](bbox=[0.14, 0.26, 0.24, 0.3])

If you use the > redirection operator and send the output to a file that already exists, that file’s current data will be deleted. Use caution when employing this operator.

To append data to a preexisting file, you need to use a slightly different redirection operator. The >> operator will append data to a preexisting file. If the file does not exist, it is created and the outputted data is added to it. Listing 4.15 shows an example of using this redirection operator.

# Listing 4.15: Using a STDOUT redirection operator to append text

```
$ echo "Nov 16, 2019" > AccountAudit.txt
$
$ wc -L /etc/passwd >> AccountAudit.txt
$
$ cat AccountAudit.txt
Nov 16, 2019
44 /etc/passwd
$
```

The first command in Listing 4.15 puts a date stamp into the AccountAudit.txt file. Because that date stamp needs to be preserved, the next command appends STDOUT to the file using the >> redirection operator. The file can continue to be appended to using the >> operator for future commands.

# Redirecting Standard Error

Another handy item to redirect is standard error. The file descriptor that identifies a command or script file error is 2. It is also identified by the abbreviation STDERR, which describes standard error. STDERR, like STDOUT, is by default sent to your terminal (/dev/tty).

The basic redirection operator to send STDERR to a file is the 2> operator. If you need to append the file, use the 2>> operator. Listing 4.16 shows an example of redirecting standard error.