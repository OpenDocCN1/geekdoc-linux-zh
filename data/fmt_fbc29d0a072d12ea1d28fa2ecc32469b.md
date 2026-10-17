
当消费者轮询提供者并使用 `refreshOnly` 操作时，它使用 LDAP Search 请求并根据搜索结果更新其自己的信息。当搜索操作完成后，提供者会发送一个 `SearchResult` 控制消息。

另一方面，当使用 `refreshAndPersist` 操作时，消费者也开始向提供者发送一个 LDAP Search 请求。在这种情况下，在返回搜索结果后，该操作在提供者中保持持久化，这样提供者中的任何后续更新都会发送给消费者。

除了这些提供者-消费者的复制模型外，我们还可以拥有多主复制，其中数据被复制到多个服务器。

### 准备工作

为了使复制工作，两个（或多个）服务器需要具有相同的时间并能够解析对方的名称。网络中解析名称的首选方法是使用带有一个或多个服务器的 DNS 基础设施，但我们使用本地 `hosts` 文件。

一旦我们检查名称解析工作正常，我们需要在新的副本机器上安装 OpenLDAP 服务器。然后，我们需要添加管理员用户，使用与我们在第一个 OpenLDAP 服务器中相同的密码，并授予该用户适当的权限。我们还为我们的域名 `linuxaholics.com` 创建了一个条目，以及用户的 `OU`，这正是我们稍后要复制的 LDAP 分支。所有这些工作已经在第一个 OpenLDAP 服务器（第 1 章）中完成，因此此时不应该没有问题。

虽然这对于复制工作来说不是绝对必要的，但为新服务器设置安全访问始终是一个好主意，就像我们之前在第一个 OpenLDAP 服务器（第 2 章）中做的那样。我们已经在 `alpha.linuxaholics.com` 计算机上了一个 CA，我们将为副本服务器创建一个新的密钥和证书。

```bash
[root@alpha CA]# openssl genrsa -out /etc/pki/CA/private/foxtrot.linuxaholics.com
Generating RSA private key, 2048 bit modulus
++++++++++++++++++++++++++++++++++++++++
```

```bash
[root@alpha CA]# openssl req -new -key /etc/pki/CA/private/foxtrot.linuxaholics.com
```

```bash
[root@alpha CA]# openssl req -new -key /etc/pki/CA/private/foxtrot.linuxaholics.com -out /etc/pki/CA/certs/foxtrot.linuxaholics.csr
Generating RSA private key, 2048 bit modulus
++++++++++++++++++++++++++++++++++++++++
```

```bash
Country Name []: ES
State or Province Name []: Madrid
Organization Name []: linuxaholics
Common Name []: foxtrot.linuxah.com
```

```bash
[root@alpha CA]# openssl ca -batch -in /etc/pki/CA/certs/foxtrot.linuxaholics.csr -key /etc/pki/CA/private/ca.key -out /etc/pki/CA/certs/foxtrot.linuxaholics.crt
```

```bash
uid: Bill
cn: Bill Windows
sn: Windows
userPassword: e1NBUox9Qm1sbEBsaW51eGFob2xpY3MuY29t

# search result
search: 2
result: 0 Success

# numResponses: 2
# numEntries: 1
[root@alpha ldap]#
```
正如我们所见，一切都按预期工作，OpenLDAP 服务器已能够将身份验证委托给 Active Directory。

### 总结

在本章中，我们向前迈了一步，以继续整合不同的系统。我们学习了 SSO 的概念并实现了用于许多 SSO 解决方案的 Kerberos。我们还查看了如何从 Windows 计算机向 OpenLDAP 服务器进行身份验证，以及如何在 OpenLDAP 中将身份验证委托给 Active Directory 服务器。

# 第 5 章

## OpenLDAP 复制

通过像 LDAP 这样的公共中央库对每个用户进行身份验证有许多优势，但也存在一些陷阱。在这种情况下，LDAP 服务器将成为单点故障，在某些情况下还可能成为瓶颈。因此，出于性能和容错性考虑，建议拥有两个或多个 OpenLDAP 服务器。

显然，每个 OpenLDAP 服务器中的信息必须保持一致，因此我们需要在它们之间配置一些复制程序。

在本章中，我们将涵盖以下概念：

- 复制概念。
- 配置 OpenLDAP 复制。
- 了解副本枢纽。
- LDAP 引用。
- LDAP 同步复制。

我们还将介绍以下术语和工具：主/从服务器、多主复制、消费者、副本枢纽、单次方法、`syncrepl`、基于拉取/推送的同步、`refreshOnly` 和 `refreshAndPersist` 以及 `replog`。

### 复制概念

到为止，我们使用的是单个 LDAP 服务器。这对于实验环境来说是一个可以接受的解决方案，但如果我们在生产环境中工作，就需要某种程度的容错性，因此我们必须向基础设施中添加（至少）另一个 LDAP 服务器。

显然，存储在 LDAP 中的信息在两个服务器中必须是相同的，因此我们需要将在一个服务器上做的更改复制到另一个或多个多个服务器上。

# 第 5 章 OpenLDAP 复制

在 OpenLDAP 的早期版本中，使用 `master`（主）和 `slave`（从）术语。更新在主服务器上进行，然后主服务器更新从服务器。这种模型是非常僵化的，角色定义非常明确。然而，在最近版本中，OpenLDAP 支持多种复制拓扑结构，以前术语已被 `provider`（提供者）和 `consumer`（消费者）取代。提供者将目录更新传播到一个或多个消费者。同一台服务器可以同时作为消费者和提供者。

复制可以通过多种方式完成。有几种可以与 OpenLDAP 使用的复制模型，我们将在整书中介绍它们。目前，在 OpenLDAP 服务器之间复制信息的推荐方法是使用 LDAP 同步复制引擎，简称为 `syncrepl`。

`syncrepl` 是一个客户端复制引擎，它允许消费者/从 LDAP 服务器保留目录信息树（DIT）片段的副本。它作为 `slapd` 服务的一个线程运行，通过连接到提供者/主服务器来执行初始加载，并定期轮询以更新内容更改，从而维护消费者副本。

`syncrepl` 使用 LDAP 内容同步协议（LDAP Sync），该协议支持基于拉取和基于推送的复制。在基于拉取的复制中，消费者向提供者轮询更新；另一方面，在基于推送的复制中，提供者本身将更新发送给消费者。LDAP Sync 通过定义两个同步操作：`refreshOnly` 和 `refreshAndPersist` 来支持这些复制模式。
