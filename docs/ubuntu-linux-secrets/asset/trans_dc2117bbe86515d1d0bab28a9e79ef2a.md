

第一个文件已经存在于 /etc/bind 文件夹中。你需要做的只是添加两个定义来指向你的区域和反向查找文件。以下是为你的网络配置 named.conf.local 文件所需的步骤：

- 1. 在文本编辑器中打开 /etc/bind/named.conf.local 文件。如果你正在 Ubuntu 服务器上工作，你需要使用命令行编辑器来完成此操作。vim 编辑器默认安装在 Ubuntu 服务器上，应该可以正常工作：
  
  sudo vim /etc/bind/named.conf.local

- 2. 添加指向区域配置文件 的区域定义。区域定义定义了域名，以及 DNS 服务器的类型（master）和区域配置文件的名称：
  
  zone "smallorg.org" {
      type master;
      file "/etc/bind/db.smallorg.org";
  };
  
  行末的分号很重要——它们表示一行的结束。

- 3. 添加指向反向查找配置文件的区域定义。反向查找配置使用反向 IP 地址格式来定义网络：
  
  zone "0.0.10.in-addr.arpa" {
      type "master";
      file "/etc/bind/db.10";
  };
  
  同样，区域文件中的每一行都必须以分号结尾。

- 4. 保存 named.conf.local 文件并退出文本编辑器。保存文件并退出编辑器的 Vim 命令是 ZZ。

一旦你更新了 named.conf.local 文件，你就可以创建你的区域配置和反向查找配置文件了。首先，以下是创建区域配置文件的步骤：

- 1. 使用文本编辑器创建一个名为 /etc/bind/db.smallorg.org 的新文件。如果你指定 vim 命令行中的文件名，vim 编辑器将自动为你创建它：
  
  sudo vim /etc/bind/db.smallorg.org

- 2. 为你的区域添加 SOA 记录。SOA 记录需要命名你的 DNS 服务器，以及管理员账户的电子邮件地址（请记住在电子邮件地址中用点代替 @ 符号，并且还请记住在 DNS 服务器名称末尾加上一个点）。示例如下：
  
  @ IN SOA testbox.smallorg.org. postmaster.smallorg.org. (
  2008010151 ; serial, todays date + todays serial #
  3600 ; refresh, seconds
  1800 ; retry, seconds
  604800 ; expire, seconds
  3600 ) ; minimum, seconds

- 3. 添加 NS 记录来定义域名的名称服务器。NS 记录指向运行 DNS 的 Ubuntu 服务器的名称：
  
      NS testbox : name server

- 4. 添加任何 MX 记录以指向网络上的邮件服务器。邮件服务器可以用相同的优先级（以实现负载均衡）或不同的优先级（以定义主邮件服务器和辅助邮件服务器）来广告。邮件服务器不必位于你的网络上。
  
      MX 10 mail.smallorg.org. : Primary mail server
      MX 20 mail.isp.net. : Secondary mail server at ISP

- 5. 添加 A 记录来定义你希望向互联网广告的本地网络上的主机，以及任何 CNAME 记录来定义别名。此区域需要列出网络上的所有主机：
  
      www CNAME fred.smallorg.org : defines the Web host alias
      localhost A 127.0.0.1
      testbox A 10.0.0.1 : defines the DNS server
      fred A 10.0.0.2 : defines Web server
      mail A 10.0.0.3 : defines the mail host

- 6. 保存文件并退出编辑器。保存文件并退出编辑器的 vim 命令是 ZZ。

现在你已经 halfway 托管你的域名了！接下来你必须为 named.conf.local 文件中列出的反向域名地址创建 DNS 数据库文件。以下是执行此操作的步骤：

- 1. 使用文本编辑器创建 /etc/bind/db.10 文件。文件名中的数字必须与你的网络 IP 地址的第一个八位字节匹配。同样，你可以使用 vim 编辑器创建文件：
  
      sudo vim /etc/bind/db.10

- 2. 添加 SOA 记录来定义你的网络。你可以使用区域配置文件中使用的相同 SOA 记录：
  
      @ IN SOA testbox.smallorg.org. postmaster.smallorg.org. (
      2008810151 ; serial, todays date + serial #
      3600 ; refresh, seconds
      1800 ; retry, seconds
      604800 ; expire, seconds
      3600 ) ; minimum, seconds

- 3. 添加 NS 记录来定义域名的名称服务器。NS 记录指向运行 DNS 的 Ubuntu 服务器的名称：
  
      NS testbox : name server

- 4. 为区域配置文件中定义的每个主机添加 PTR 记录。可能需要反向查找的每个主机都应添加到此列表中，并附带其在网络上的 IP 地址的主机部分：
  
      1 PTR testbox.smallorg.org.
      2 PTR fred.smallorg.org.
      3 PTR mail.smallorg.org.

- 5. 保存文件并退出编辑器。保存并退出的 vim 命令是 ZZ。

