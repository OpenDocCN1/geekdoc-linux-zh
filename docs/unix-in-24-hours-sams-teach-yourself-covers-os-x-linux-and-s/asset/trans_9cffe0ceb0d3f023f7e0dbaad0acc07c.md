

输入消息并以 ^d 结束，就像在任何电子邮件消息中一样。它会立即发送给我。

## Note

我邀请你给我写个便条，告诉我你对这本书的感受，你可能遇到的任何问题，以及任何让你困惑的命令，如果多解释一点会更容易理解。至少，问个好！

## 2. 尽管电子邮件地址始终遵循相同的格式，但它们可能变化很大。为了让你了解这种变化程度，这里有一些我最近收到的邮件中的地址拼凑（已更改细节以保护隐私）：

Click here to view code image

```
$ grep '^From:' /usr/spool/mail/taylor
From: Steve Frampton <frampton@vicuna.ocunix.on.ca>
From: Joanna Tsang <tsang@futon.SFSU.EDU>
From: "Debra Issleris" <disserli@us.oracle.com>
From: ljw@ras.amdahl.com (Linda Wei)
From: Cheryl <CBUTCHER@VM.CC.PURDUE.EDU>
From: harris@mace.utech.edu (Mickey Harris)
From: v892127@nooteboom.si.hhs.nl
From: harris@mace.utech.edu (Mickey Harris)
From: "Barbara Maxwell" <maxwell@sales.synergy.com>
From: steve@xalt.com (Steve Mansour)
From: abhasin@itsmail1.hamilton.edu (Aditya Bhasin)
From: gopher@scorpio.kent.edu
From: marv@netcom.com (Marvin Raab)
```

电子邮件中 From: 行的记号惯例显然各不相同。你在这个列表中看到了三种基本记号：只是地址，例如来自 gopher@scorpio.kent.edu 的地址；带括号内姓名的地址，例如列表大约三分之一处来自 Linda Wei 的消息；以及人名后跟尖括号中的电子邮件地址的行，例如第一个列出的行。

注意我过去几天收到电子邮件的各种站点：SFSU.EDU 是旧金山州立大学，oracle.com 是加州的甲骨文公司，PURDUE.EDU 是普渡大学，xalt.com 来自 XALT 公司，kent.edu 是肯特州立大学。来自 v892127@nooteboom.si.hhs.nl 的消息来自荷兰的一所教育机构！

## 3. 你如何将域名映射到组织？这在命令行上也出奇地容易，使用 whois 命令。让我们来看看，但首先，有一个警告：whois 程序中的免责声明太多了，它会产生大约 75 行输出，而我们感兴趣阅读的 10 行通常被埋在其中，所以通常需要做一些侦探工作。

这是对域名 ISIPP.COM 的样子：

Click here to view code image

```
$ whois isipp.com
```

Whois Server Version 2.0

Domain names in the .com and .net domains can now be registered with many different competing registrars. Go to http://www.internic.net for detailed information.

Domain Name: ISIPP.COM
Registrar: GODADDY.COM, LLC
Sponsoring Registrar IANA ID: 146
Whois Server: whois.godaddy.com
Referral URL: http://registrar.godaddy.com
Name Server: A.AUTH-NS.SONIC.NET
Name Server: B.AUTH-NS.SONIC.NET
Name Server: C.AUTH-NS.SONIC.NET
Name Server: NS.ISIPP.COM
Name Server: NS2.PRGM R.COM
Name Server: NS3.PRGM R.COM
Status: clientDeleteProhibited http://www.icann.org/epp#clientDeleteProhibited
Status: clientRenewProhibited http://www.icann.org/epp#clientRenewProhibited
Status: clientTransferProhibited http://www.icann.org/epp#Prohibited
Status: clientUpdateProhibited http://www.icann.org/epp#clientUpdateProhibited
Updated Date: 15-apr-2015
Creation Date: 17-aug-2003
Expiration Date: 17-aug-2023

>>> Last update of whois database: Mon, 18 May 2015 22:34:58 GMT <<<

NOTICE: The expiration date displayed in this record is the date the registrar’s sponsorship of the domain name registration in the registry is currently set to expire. This date does not necessarily reflect the expiration date of the domain name registrant’s agreement with the sponsoring registrar. Users may consult the sponsoring registrar’s Whois database to view the registrar’s reported date of expiration for this registration.

TERMS OF USE: You are not authorized to access or query our Whois database through the use of electronic processes that are high-volume and automated except as reasonably necessary to register domain names or modify existing registrations; the Data in VeriSign Global Registry Services’ (“VeriSign”) Whois database is provided by VeriSign for information purposes only, and to assist persons in obtaining information about or related to a domain name registration record. VeriSign does not guarantee its accuracy. By submitting a Whois query, you agree to abide by the following terms of use: You agree that you may use this Data only for lawful purposes and that under no circumstances will you use this Data to: (1) allow, enable, or otherwise support the transmission of mass unsolicited, commercial advertising or solicitations via e-mail, telephone, or facsimile; or (2) enable high volume, automated, electronic processes that apply to VeriSign (or its computer systems). The compilation, repackaging, dissemination or other use of this Data is expressly prohibited without the prior written consent of VeriSign. You agree not to use electronic processes that are automated and high-volume to access or query the Whois database except as reasonably necessary to register domain names or modify existing registrations. VeriSign reserves the right to restrict your access to the Whois database in its sole discretion to ensure operational stability. VeriSign may restrict or terminate your access to the

