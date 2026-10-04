
# 第 20 章 FTP：跨网络传输文件

尽管他在 `dog` 上的用户名是 `sam`，他在响应 `Name (dog):` 提示时输入了 `sam`。Sam 在 `Password:` 提示处输入了他的普通系统密码，`vsftpd` 服务器给了他信息 Entering Passive Mode (192,168,0,12,130,201)

150 Here are the directory listing.

drwxr-xr-x 2 1001 1001 4096 Jan 25 04:51:25 expenses

drwxr-xr-x 2 1001 1001 4096 Jan 25 04:53:55 memos

drwxr-xr-x 2 1001 1001 4096 Jan 25 04:51:57 tech

226 Directory OK.

```
sam@plum:~ $ ftp dog
Connected to dog.bogus.com.
220 (vsFTPd 2.0.4)
Name (dog:sam): sam
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp:
```

登录后，Sam 使用 `ftp` 命令查看他远程工作目录中的内容，该目录是 `dog` 上的主目录。然后他 `cd` 进入 `memos` 目录并显示那里的文件。

## ls 和 cd

```
ftp> ls
227 Entering Passive Mode (192,168,0,12,130,201)
150 Here are the directory listing.
drwxr-xr-x 2 1001 1001 4096 Jan 25 04:51:25 expenses
drwxr-xr-x 2 1001 1001 4096 Jan 25 04:53:55 memos
drwxr-xr-x 2 1001 1001 4096 Jan 25 04:51:57 tech
226 Directory OK.
```

## FTP CLIENT 733

```
ftp> cd memos successfully changed.
250 Directory successfully changed.

ftp> ls
227 Entering Passive Mode (192,168,0,12,48,84)
150 Here comes the directory listing.
-rw-r--r-- 1001 1001 3430 Jan 25 04:52 memo.0514
-rw-r--r-- 1001 1001 6581 Jan 25 04:52 memo.0628
-rw-r--r-- 1001 1001 2801 Jan 25 04:52 memo.0905
-rw-r--r-- 1001 1001 7351 Jan 25 04:53 memo.0921
-rw-r--r-- 1001 1001 14703 Jan 25 04:53 memo.1102
226 Directory send OK.
ftp>
```

接下来，Sam 使用 `ftp` 命令将 `memo.1102` 从服务器复制到本地系统。他使用二进制模式确保了无论文件是二进制还是 ASCII 格式，都能获得该文件的良好副本。服务器确认文件已成功复制，并报告了其大小和复制所需的时间。随后，Sam 将本地文件 `memo.1114` 复制到远程系统。该文件被复制到他的远程工作目录 `memos` 中。

```
ftp> get memo.1102
local: memo.1102 remote: memo.1102
227 Entering Passive Mode (192,168,0,12,53,74)
150 Opening BINARY data connection for memo.1102 (14703 bytes).
226 File send OK.
14703 bytes received in 0.00 secs (11692.5 kb/s)

ftp> put memo.1114
local: memo.1114 remote: memo.1114
227 Entering Passive Mode (192,168,0,12,182,124)
150 Ok to send data.
226 File receive OK.
11903 bytes in 0.00 secs (23294.6 kb/s)
ftp>
```

现在，Sam 决定将 `memos` 中的所有文件复制到本地系统上的新目录。他输入了一个 `ls` 命令以确保复制了正确的文件，但 ftp 超时了。他没有退出 ftp 并向服务器发送另一个 `ftp` 命令，而是输入了 `open` 命令重新连接到服务器。登录后，他使用 `ftp` 命令切换目录到 `memos`。

```
ftp> ls
No control connection: Success.
ftp> open dog
Connected to dog.bogus.com.
220 (vsFTPd 2.0.4)
Name (dog:sam): sam
ftp> cd memos
250 Directory successfully changed.
ftp>
```
