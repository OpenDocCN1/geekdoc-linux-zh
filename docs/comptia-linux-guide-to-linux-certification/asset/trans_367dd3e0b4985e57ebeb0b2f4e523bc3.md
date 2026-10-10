
### 项目 13-7

在这个动手实践项目中，您将安装并配置 Very Secure FTP 守护进程到您的 Ubuntu Server Linux 虚拟机上。

- 1. 在您的 Ubuntu Server Linux 虚拟机上，使用用户名 **root** 和密码 LNXrocks! 登录到 tty1。
- 2. 在命令提示符下，输入 `apt-get install vsftpd` 并按 **Enter** 键安装 vsftpd。
- 3. 在命令提示符下，输入 `cp /etc/hosts user1/file1 ; cp /etc/hosts user1/file2 ; cp /etc/hosts /srv/ftp/file3` 并按 **Enter** 键，在 user1 的主目录中创建 /etc/hosts 文件的两个副本，分别命名为 file1 和 file2，并在 /srv/ftp 目录中创建 /etc/hosts 文件的一个副本，命名为 file3。
- 4. 使用 vi 编辑器编辑 /etc/vsftpd.conf 文件。花一点时间阅读该文件中的选项以及描述每个选项的注释。接下来，取消注释 `write_enable=YES` 这一行，将 `anonymous_enable` 行修改为 `anonymous_enable=YES`，保存更改并退出 vi 编辑器。
- 5. 在命令提示符下，输入 `service vsftpd restart` 并按 **Enter** 键重启 vsftpd。
- 6. 在命令提示符下，输入 `ftp localhost` 并按 **Enter** 键。当提示时，使用密码 LNXrocks! 以 **user1** 的身份登录。
- 7. 在 ftp> 提示符下，输入 `dir` 并按 **Enter** 键列出 /home/user1 目录的内容。
- 8. 在 ftp> 提示符下，输入 `lcd /etc` 并按 **Enter** 键将 FTP 客户端上的当前工作目录更改为 /etc。
- 9. 在 ftp> 提示符下，输入 `put issue` 并按 **Enter** 键将 issue 文件上传到远程 FTP 服务器。
- 10. 在 ftp> 提示符下，输入 `dir` 并按 **Enter** 键列出 /home/user1 目录的内容。issue 文件是否成功上传？
- 11. 在 ftp> 提示符下，输入 `lcd /` 并按 **Enter** 键将 FTP 客户端上的当前工作目录更改为 /。
- 12. 在 ftp> 提示符下，输入 `get issue` 并按 **Enter** 键将 issue 文件下载到本地计算机的 / 目录。
- 13. 在 ftp> 提示符下，输入 `mget file*` 并按 **Enter** 键将 file1 和 file2 下载到本地计算机的 / 目录。
- 14. 在 ftp> 提示符下，输入 `help` 并按 **Enter** 键列出 FTP 客户端程序中可用的命令。
- 15. 在 ftp> 提示符下，输入 `bye` 并按 **Enter** 键退出 FTP 客户端程序。
- 16. 在命令提示符下，输入 `ls /` 并按 **Enter** 键。issue、file1 和 file2 文件是否成功下载到 / 目录？
- 17. 在命令提示符下，输入 `ftp localhost` 并按 **Enter** 键。当提示时，使用密码 **nothing** 以 **anonymous** 身份登录（对于匿名用户，实际密码并不重要；您可以使用任何密码）。
- 18. 在 ftp> 提示符下，输入 `dir` 并按 **Enter** 键列出 /var/ftp 目录的内容。
- 19. 在 ftp> 提示符下，输入 `lcd /` 并按 **Enter** 键将 FTP 客户端上的当前工作目录更改为 /。
- 20. 在 ftp> 提示符下，输入 `get file3` 并按 **Enter** 键将 hosts 文件下载到本地计算机的 / 目录。
- 21. 在 ftp> 提示符下，输入 `bye` 并按 **Enter** 键退出 FTP 客户端程序。
- 22. 在命令提示符下，输入 `ls /` 并按 **Enter** 键。file3 是否成功下载到 / 目录？
- 23. 在命令提示符下，输入 `ftp localhost` 并按 **Enter** 键。当提示时，使用密码 **LNXrocks!** 以 **root** 用户登录。您能够登录吗？在 ftp> 提示符下，输入 `bye` 并按 **Enter** 键退出 FTP 客户端程序。
- 24. 使用 vi 编辑器编辑 /etc/ftpusers 文件并删除以下行：
    root
    完成后，保存更改并退出编辑器。
- 25. 在命令提示符下，输入 `ftp localhost` 并按 **Enter** 键。当提示时，使用密码 **LNXrocks!** 以 **root** 用户登录。
- 26. 在您的 Windows 主机上，从 https://filezilla-project.org/ 下载并安装免费的 FileZilla FTP 客户端程序。接下来，打开 FileZilla 程序并在 Host 对话框中输入 IP Address（其中 *IPaddress* 是您 Ubuntu Server Linux 虚拟机的 IP 地址）。接下来，在 Username 对话框中输入 *user1*，在 Password 对话框中输入 *LNXrocks!*，并单击 Quickconnect。探索在您的 Windows 主机和 Ubuntu Server Linux 虚拟机之间复制文件，完成后关闭 FileZilla。

### 项目 13-8

在这个动手实践项目中，您将探索您 Ubuntu Server Linux 虚拟机上的 Postfix 电子邮件守护进程。

- 1. 在您的 Ubuntu Server Linux 虚拟机上，使用用户名 **root** 和密码 LNXrocks! 登录到 tty1。
- 2. 在命令提示符下，输入 `ps -ef | grep postfix` 并按 **Enter** 键。Postfix 守护进程是否正在运行？
- 3. 使用文本编辑器编辑 /etc/aliases 文件并添加以下行：
    webmaster: user1
    完成后，保存更改并退出编辑器。
- 4. 在命令提示符下，输入 `newaliases` 并按 **Enter** 键，使用 /etc/aliases 文件中的信息更新别名数据库。
- 5. 在命令提示符下，输入 `mail webmaster` 并按 **Enter** 键，向用户 admin 和 user1 撰写新邮件。当提示输入主题时，输入 `Test email` 并按 **Enter** 键。接下来，输入 `This is a test email that will be delivered using the Postfix daemon` 并按 **Enter** 键。接下来，输入 `.`（一个句点）并按 **Enter** 键。再次按 **Enter** 键以完成并发送邮件。
- 6. 在命令提示符下，输入 `su - user1` 切换到作为 user1 的新 shell。
- 7. 在命令提示符下，输入 `mail` 以检查您的邮件箱中的电子邮件消息。最后一封邮件的主题应为 `Test e-mail`。如果您没有看到这条消息，请输入 `z` 以进入下一条消息屏幕。注意具有 `Test e-mail` 主题的电子邮件消息的编号，并在 `&` 提示符下输入该编号以阅读您的电子邮件消息。完成后输入 `q` 以退出邮件程序。
- 8. 在命令提示符下，输入 `exit` 并按 **Enter** 键返回到您的 root shell。
- 9. 在命令提示符下，输入 `telnet localhost 25` 并按 **Enter** 键。您能意识到自己正在与 Postfix 守护进程交互吗？
- 10. 输入 `EHLO localhost` 并按 **Enter** 键。您的 Postfix 守护进程是否支持 8 位 MIME？输入 `quit` 并按 **Enter** 键退出 telnet 会话。
- 11. 输入 `exit` 并按 **Enter** 键注销您的 shell。

### 项目 13-9

在这个动手实践项目中，您将使用您 Ubuntu Server Linux 虚拟机上的 PostgreSQL 创建、查询和管理数据库。

- 1. 在您的 Ubuntu Server Linux 虚拟机上，使用用户名 **root** 和密码 LNXrocks! 登录到 tty1。
- 2. 在命令提示符下，输入 `psql - postgres` 并按 **Enter** 键。在两个提示处输入密码 **LNXrocks!** 并按 **Enter** 键，为 postgres 用户账户设置密码 **LNXrocks!**。
- 3. 在命令提示符下，输入 `su - postgres` 并按 **Enter** 键，以 postgres 用户身份启动新 shell。
- 4. 在命令提示符下，输入 `createdb sales` 并按 **Enter** 键。
- 5. 在命令提示符下，输入 `psql sales` 并按 **Enter** 键启动 PostgreSQL 实用工具。
- 6. 在 `sales=#` 提示符下，输入 `\l` 并按 **Enter** 键查看您 PostgreSQL 服务器上的数据库。postgres 数据库存储 PostgreSQL 服务器内部使用的信息，而 template 数据库在创建新数据库时使用。注意，您的 sales 数据库已列出，并用于信息的 UTF-8 字符集。
- 7. 在 `sales=#` 提示符下，输入 `CREATE TABLE customer (Name char(20), Address char(40), Balance char(10) );` 并按 **Enter** 键创建一个包含三个字段（Name, Address, Balance）的 customer 表。
- 8. 在 `sales=#` 提示符下，输入 `\d` 并按 **Enter** 键查看您数据库中的表。是否列出了 customer 表？
- 9. 在 `sales=#` 提示符下，输入 `\d customer` 并按 **Enter** 键查看 customer 表中的字段。每个字段允许多少个字符？
- 10. 在 `sales=#` 提示符下，输入 `INSERT INTO customer VALUES ('Lily Bopoo','123 Rutherford Lane','526.80');` 并按 **Enter** 键向您的表添加一条记录。
- 11. 在 `sales=#` 提示符下，输入 `INSERT INTO customer VALUES ('Lily Bopoo','123 Rutherford Lane','526.80');` 并按 **Enter** 键向您的表添加一条记录。
- 12. 在 `sales=#` 提示符下，输入 `INSERT INTO customer VALUES ('Harvey Lipshitz','51 King Street','122.19');` 并按 **Enter** 键向您的表添加一条记录。
- 13. 在 `sales=#` 提示符下，输入 `INSERT INTO customer VALUES ('John Escobar','14-6919 Franklin Drive','709.66');` 并按 **Enter** 键向您的表添加一条记录。
- 14. 在 `sales=#` 提示符下，输入 `SELECT * from customer;` 并按 **Enter** 键查看您表中的所有记录。
- 15. 在 `sales=#` 提示符下，输入 `SELECT * from customer ORDER BY Balance DESC;` 并按 **Enter** 键按余额降序查看您表中的所有记录。
- 16. 在 `sales=#` 提示符下，输入 `SELECT * from customer WHERE Name='Harvey Lipshitz';` 并按 **Enter** 键查看 Harvey Lipshitz 的记录。
- 17. 在 `sales=#` 提示符下，输入 `CREATE USER bob WITH PASSWORD 'supersecret';` 并按 **Enter** 键在 PostgreSQL 中创建一个可以访问 customer 数据库的用户账户。
- 18. 在 `sales=#` 提示符下，输入 `GRANT ALL PRIVILEGES ON customer TO bob` 并按 **Enter** 键授予 bob 用户 customer 表的 SELECT, UPDATE, DELETE, 和 INSERT 权限。

