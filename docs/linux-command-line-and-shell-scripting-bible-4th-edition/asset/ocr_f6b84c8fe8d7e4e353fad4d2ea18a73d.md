```
```python
> print $0}'
My name is Rich
My name is Christine
$
```
```

After we opened with a single quotation mark, the Bash shell provided the secondary prompt to prompt us for more data. We added our commands one at a time on each line until we entered the closing single quotation mark. Because no filename was defined in the command line, the `gawk` program retrieves data from `STDIN`. When we ran the program, it waited for text to come in via STDIN. To exit the program, we pressed the `Ctrl+D` key combination to signal the end of the data and get back to a shell prompt.

# ## Reading the program from a file

Like the `sed` editor, the `gawk` editor allows you to store your programs in a file and refer to them in the command line:

```
```
$ cat script2.gawk
{print $1 "'s home directory is " $6}
$
$ gawk -F: -f script2.gawk /etc/passwd
root's home directory is /root
daemon's home directory is /usr/sbin
bin's home directory is /bin
[...]
christine's home directory is /home/christine
sshd's home directory is /run/sshd
$
```
```

The `script2.gawk` program script uses the `print` command again to print the `/etc/passwd` file's home directory data field (field variable `$6`) and the user name data field (field variable `$1`).

You can specify multiple commands in the program file. To do so, just place each command on a separate line. You don't need to use semicolons:

```
```
$ cat script3.gawk
{
 text = "'s home directory is "
 print $1 text $6
}
$
```
```