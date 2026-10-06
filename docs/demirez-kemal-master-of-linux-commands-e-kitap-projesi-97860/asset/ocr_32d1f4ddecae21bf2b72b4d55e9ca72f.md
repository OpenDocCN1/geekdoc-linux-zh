+   * cat test-2 We saw what we type last is added to the file content.

+   * cat > test-2 (Please note that we use > only once) we add our new content in our file.

+   * cat test-2 When we checked again with the content of our files, we found that the old content is deleted and the content we enter the final written.

We learn that we can read the file content with cat command. If we use cat command with -A the tab in the text shows spaces with ^, and shows ends of the line with $.

```
root@kemal:~/zeyno# cat >> test
Debian Whezy
root@kemal:~/zeyno# cat -A test
Kali Linux 2.0 (Kali Sana)
^IDebian^IWhezy$
root@kemal:~/zeyno# _
```

To change lowercase letters to uppercase letters in a text file that we want to see the contents or to do the opposite, we can use cat and tr command together. For example, to change lowercase letters to uppercase letters in test file, we can use cat test | tr 'a-z' 'A-Z'.

```
root@kemal:~/zeyno# cat test
Kali Linux 2.0 (Kali Sana)
Debian Whezy
root@kemal:~/zeyno# cat test | tr 'a-z' 'A-Z'
KALI LINUX 2.0 (KALI SANA)
DEBIAN WHEEZY
root@kemal:~/zeyno# _
```