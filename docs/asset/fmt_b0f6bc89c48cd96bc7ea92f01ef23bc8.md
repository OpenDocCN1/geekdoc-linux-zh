
邮件的源将类似于下面输出中显示的文本，但请注意，为了保持简单，此示例中删除了大量信息。这是一封从 sender@example.com 发送到 recipient@hacker.house 的邮件。该邮件是从 hacker@house 的视角查看的。

```
Delivered-To: recipient@hacker.house
Received: by 2002:ac12be9:0:0:0 with SMTP ID n54csp7145050qn;
Mon Jan 21 2019 11:14:05 -0800 (PST)
Return-Path: <sender@example.com>
Received: from wout2-smtp.messagingengine.com (wout2-smtp
mmagingengine.com) with (64.147.125.25)
by my.google.com with ESMTPS ID u2si238383
qa.125.2019.01.21.11.14.05
Received: for <recipient@hacker.house>
(version=TLS1.2;cipher=ECDHE-RSA-AES128-GCM-SHA256)
bits=128;
Received: Mon Jan 21 2019 11:14:05 -0800 (PST)
Received-SPF: pass (google.com: domain of sender@example.com designates in
64.147.125.25)
```

# 邮件头

邮件在旅程中经过的每一个系统都会在邮件中留下一点自己的痕迹，当然，不是在邮件正文中，而是在头文件中，那里对普通用户来说是不可见的。通常可以识别不同系统在邮件旅程到元数据过程中所使用的技术和软件。甚至可能确定收件人正使用什么类型的杀病毒软件扫描邮件，如果你需要规避检测，这是一个非常有价值的信息。只要知道点击哪些按钮，任何人都可以查看这些信息。邮件客户端提供了查看邮件消息源的选项，就像浏览器允许你查看网页源代码一样。

邮件的源将类似于下面输出中显示的文本，但请注意，为了保持简单，此示例中删除了大量信息。这是一封从 sender@example.com 发送到 recipient@hacker.house 的邮件。该邮件是从 hacker@house 的视角查看的。

```
Delivered-To: recipient@hacker.house
Received: by 2002:ac12be9:0:0:0 with SMTP ID n54csp7145050qn;
Mon Jan 21 2019 11:14:05 -0800 (PST)
Return-Path: <sender@example.com>
Received: from wout2-smtp.messagingengine.com (wout2-smtp
mmagingengine.com) with (64.147.125.25)
by my.google.com with ESMTPS ID u2si238383
qa.125.2019.01.21.11.14.05
Received: for <recipient@hacker.house>
(version=TLS1.2;cipher=ECDHE-RSA-AES128-GCM-SHA256)
bits=128;
Received: Mon Jan 21 2019 11:14:05 -0800 (PST)
Received-SPF: pass (google.com: domain of sender@example.com designates in
64.147.125.25)
```

## 第6章 ■ 电子邮箱

报告的第一部分（未）包含了一条友好的信息，其中包含的目标软件名称是——Office365。

### 原始邮件头信息

```
Received: from AMSPR06CA0010.eurprd0.prod.outlook.com (2603:10a6:206:2:23)

by V1PR062MB3693.eurprd0.prod.outlook.com (2603:10a6:803:16::22)

with Microsoft SMTP Server (version=TLS1_2, cipher=TLS_ECDHE_RSA_WITH_256_GCM_SHA384) id 15.20.1558:19; Tue, 29 Jan 2019 12:25:04 +0000

Received: from DBE5UR01FT053.exe-EUR01.prod.protection.outlook.com (2401:f11:411.45:7e0::229) by AMSPR06CA0010.outlook.com.office365.com (2603:10a6:206:2:23) with Microsoft SMTP Server (version=TLS1_2, cipher=TLS_ECDHE_RSA_WITH_256_CBC_SHA384) id 15.20.1580:16 via Frontend Transport: Tue, 29 Jan 2019 12:25:03 +0000

Authentication-Results: spf=pass (sender IP is 66.111.4.25) smtp.mailfrom=hacker.example;target.example; dkim=pass (signature verified) header.hacker.example;target.example; dmarc=pass action=none header.from=hacker.example;

Received-SPF: Pass (protection.outlook.com; domain of hacker.example designates 66.111.45 as permitted sender) receiver=outlook.com; client-ip=66.111.4.25; hello=out-smtp.messagingengine.com;

Received: from-smtp.messagingengine.com (66.111.4.25) by DBE5UR01FT053.mail.protection.outlook.com (10.152.15.9) with Microsoft id id id Server (version=TLS1_2, cipher=TLS_ECDHE_RSA_WITH_256_CBC_SHA384) 15.20.1580.10 via Frontend Transport; Tue, 29 Jan 2019 12:25:03 +0000

Received: from compute2.internal (compute2.ny.internal) [10.202.2.1] by mailoy.ny.internal (Postfix) with ESMTP id 82F3725163 for <admin@target.example>; Tue, 29 Jan 2019 07:25:02 -0500 (EST)

Received: from mailfront4db[10.202.2.1] by compute2.internal (MEYROC); Tue, 29 Jan 2019 07:25:02 -0500

Received: from [10.0.1.18] (82-132-246-223.02) [82,132,246,223] by mail.messagingengine.com (Postfix) with ESMTPA id B1AE84E1F3 for <admin@target.example>; Tue, 29 Jan 2019 07:25:01 -0500

To: admin@target.example

From: Hacker <hacker@hacker.example>

Subject: test

Message-ID: <be6bd0c9-4ab4-4bd0-1a25-a8b79abe12@hacker.example>

Date: Tue, 29 Jan 2019 12:24:47 +0000

User-Agent: Mozilla/5.0 (X1; Linux x86_64; rv:60) Gecko/2010101 Thunderbird/60.4.0

MIME-Version: 1.0

Content-Type: text/plain; charset=utf-8; format=flow

Content-Transfer-Encoding: 7bit

Content-Language: en-US

Return-Path: hacker@hacker.example

Reporting-MTA: dns;61.euprprd06.prod.outlook.com
```
