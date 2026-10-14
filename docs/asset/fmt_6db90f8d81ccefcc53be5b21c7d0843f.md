
```text
$(color #EA6B36} 下载速度 $(color #E7E7E7)$downpeed eth0)${color #E7E7E7}

$(color #EA6B36} 上传速度: $(color #E7E7E7)

$(color #E7E7E7)$downspeed eth0 15, 150 00000ff)$alignr$

$(color #E7E7E7)$upspeed eth0 15, 150 0000ff ff0000)
```

```php
<?php

$remote = $_SERVER["REMOTE_ADDR"];

echo $remote;

?>
```

```bash
#!/bin/bash

sleep 45 &&

exec conky -d -c ~/conky/conkyrc &

# sleep 50 &

# exec conky -d -c ~/conky/conkyrc_weather &

exit
```

```bash
matthew@seymour:~$ cp filename filename.original
```

```bash
matthew@seymour:~$ cp filename.original filename
```

```bash
matthew@seymour:~$ sudo tar cvf etc.tar /etc
```

```bash
matthew@seymour:~$ sudo tar cv /etc > etc.tar
```

```bash
matthew@seymour:~$ sudo tar cjvf fullbackup.tar.bz2 /
```

```bash
matthew@seymour:-$ sudo find / -newer name_of_last_backup_file ! -a -type f -print
```

```bash
matthew@seymour:-$ sudo find / -newer name_of_last_backup_file ! -type d -print | \
tar czT - backup_file_name_or_device_name
```

```bash
matthew@seymour:~ sudo sudo cvzf /dev/hdd /boot /etc /home
```

```bash
matthew@seymour:~$ sudo tar czvMf /dev/fd0 /home
```

为 `/dev/fd0` 准备卷 #2 并回车：

```bash
matthew@seymour:~$ sudo tar xjvf ubuntutest.tar.bz2
```

```bash
matthew@seymour:- sudo tar tjvf ubuntuutest.tar.bz2

tar: Record size = 8 blocks

drwxr-xr-x matthew/matthew 0 2013-07-08 14:58 other/

-rwxr-xr-x matthew/matthew 1856 2013-04-29 14:37 other/matthew_helmke public.asc

-drwxr-xr-x matthew/matthew 170 2013-05-28 18:11 backup.sh

-drwxr-xr-x matthew/matthew 1593 2013-10-11 10:38 backup_method
```

```bash
matthew@seymour:~$ tar -cvf files | (cd target_directory ; tar -xpf)
```

```bash
matthew@seymour:~$ tar -cvzf data_folder | ssh remote_host '( cd -~/mybackup_dir;  tar -xzvf ) '
```

```bash
matthew@seymour:~$ cp -a source_directory target_directory
```

```bash
matthew@seymour:-$ sudo cp -avR directory_to_backup destination_vol_or_dir 1/root/backup_log.txt
```

```bash
matthew@seymour:~ sudo cp -avR ubuntu /test2 1 > /root/backup_log.txt
```

```bash
matthew@seymour~$ sudo touch backup.sh
```

```bash
from=/home/matthew-exclude.txt --backup --backup-dir='+date +%Y-%m-%d' -av / /media/externaldrive/backup/Seymour
```

```bash
matthew@seymour:~$ sudo chmod +x backup.sh
```

```bash
matthew@seymour:~ rsync --force --ignore-errors --delete --delete-excluded /media/externaldrive/backup/seymour/
```

```bash
matthew@seymour:~$ etckeeper init
```

```bash
matthew@seymour:~$ etckeeper commit "Changed prompt style"
```

```bash
mathew@semour:~$ bzr log /etc/bashrc

revno: 2

committer: mathew@seymour

branch: seymour_etc

date: 2013-07-16 11:08:22

message: Changed /etc/bashrc

revno: 1

committer: mathew@seymour

branch: seymour_etc

date: 2013-07-16 11:00:16

message: Changed /etc/bashrc
```

```bash
matthew@seymour:~$ bzr revert 2 /etc/bashrc
```

```bash
matthew@seymour:~$ sudo fdisk -l
```

```bash
matthew@seymour:~$ sudo mount /dev/sda1 /mnt
```

```bash
matthew@seymour:-$ sudo grub-install --boot-directory=/mnt /dev/sda
```

```bash
matthew@seymour:~$ sudo update-grub
```

```bash
matthew@seymour:-$ ifconfig

lo           linkenc Loopback

       inet 127.0.0.1  mask:255.0.0.0

       inet6 ::1  scope_link  UP  RUNNING  MTU:65536  metric 1

               packets:0  errors:0  overruns:0 frame

               packets:0  errors:0  overruns:0 collisions:0 txqueuelen:0

               RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

```bash
matthew@seymour:~$ sudo /sbin/ifconfig lo 127.0.0.1
```

```bash
matthew@seymour:~$ sudo /sbin/route add 127.0.0.1 lo
```

```bash
matthew@semour:~$ ping -c 3 localhost

PING localhost (127.0.0.1) 56(84) bytes of data.

64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.154 ms

64 bytes from 127.0.0.1: icmp_seq=2 ttl=64 time=0.159 ms

64 bytes from 127.0.0.1: icmp_seq=3 ttl=64 time=0.153 ms

--- localhost ping statistics

3 packets transmitted, 3 received, 0% packet loss, time 1998ms
```
