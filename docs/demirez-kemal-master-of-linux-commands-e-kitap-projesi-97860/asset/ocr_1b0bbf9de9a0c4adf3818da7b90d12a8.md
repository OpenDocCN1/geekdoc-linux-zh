# Less

Once again, to read the contents of a file, another command you can use is less command. With this command as the more command we display output with long files to easy to read. Using the up and down arrow keys to scroll through the pages. With space key, goes to next page, with b key goes to the previous page. To exit q key used is same as we mentioned before.

# Head-Tail

While viewing the file contents to see the first ten rows head, to view the last ten tail command is used. The use of these parameters is the case if you want to see a certain number of rows you must specify them with -n parameter. For example, to see the first five lines head -n 5, see the last five lines tail -n command can be used.

```
root@kemal:~# head -n 5 /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/sbin/nologin
bin:x:2:2:bin:/usr/sbin:/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:6:6534:sync:/bin/sync
root@kemal:~# tail -n 5 /etc/passwd
saned:x:129:139:/var/lib:/bin/false
usbmux:x:130:46:usbm:/var/lib/usbm:/bin/false
xfss:x:131:140:/var/lib/xfss:/bin/false
debum:x:132:142:Gnome Display Manager:/var/lib/gdm3:/bin/false
zeynep:x:1000:1001:/home/zeynep:/bin/bash
root@kemal:~-
```

# Tee

To print expressions both standard output (ie, terminal/console) and you want to write to a file specified as well,