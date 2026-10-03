# Linux Hack

Ajay Kumar Tiwari

```
for filesize in $(ls -l . | grep "^-" | awk ‘{print $5}’)
do
  let totalsize=$totalsize+$filesize
done
echo -n "$totalsize"
```

```
ramesh@dev-db ~> export PATH=$PATH:~/bin
ramesh@dev-db ~> export PS1="\u@\h
[$(totalfilesize.sh) bytes]> "
ramesh@dev-db [534 bytes]> cd /etc/mail
ramesh@dev-db [167997 bytes]>
```

[Note: This executes the totalfilesize.sh to display the total file size of the current directory in the PS1 prompt]