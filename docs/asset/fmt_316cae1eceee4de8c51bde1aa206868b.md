
频道只是一个你可以去与他人交谈的地方。IRC 上有很多频道，每个频道都专注于不同的主题。在 XChat 中，你连接的频道列表显示在窗口左侧的窗格中，所以你应该能看到你当前在 #ubuntu 中，这是用于一般 Ubuntu 帮助和支持的。你可以选中 Server > Join a Channel 来连接到另一个频道，但现在没有必要，因为我们已经在正确的频道里了。右侧窗格中列出了当前连接到同一频道的其他用户；#ubuntu 非常受欢迎，所以可能有相当多的人！

当你进入频道时，屏幕中央窗格中会有一堆消息闪过。其中前几条是自动消息，描述频道的用途、设定一些基本规则等等，但到现在你应该也能看到其他人的消息在屏幕上滚动了（Figure 20-10）。说话人的昵称在垂直分隔线的左侧，他们的消息在右侧。频道里的每个人都能看到相同的消息，通常同时进行着好几场对话。你也会在有人加入或离开频道时看到不同颜色的消息。人们一直在进进出出，所以你可以忽略这些消息。

![](img/f7cef0df22f9dba5a41777808c98eece_406_0.png)

Figure 20-10: Other users chatting in the #ubuntu IRC channel

如果你想发送消息，只需在屏幕底部的消息框中输入消息，旁边是你的昵称，然后按 ENTER。你会看到你的消息出现在中央窗格中，#ubuntu 频道里的其他人也会看到。然后你所要做的就是等待回复……

## Registering Your Nickname

最好注册你的昵称，这样别人就不能偷用它，而且下次你使用 IRC 时人们也能认出你。在窗口左侧的窗格中，点击 freenode 项目以切换到 Freenode 的欢迎频道，Freenode 是 Ubuntu 使用的 IRC 服务器（Figure 20-11）。现在，在消息框中输入`/ns register email password`，用你的电子邮件地址替换 email，用一个好密码替换 password。例如，如果这些是你的信息，输入`/ns register nopeeking joe@example.com`就能完成。按 ENTER 完成注册。

如果一切顺利，你会看到一条类似 An email containing nickname activation instructions has been sent to joe@example.com 的消息。检查你的邮件，应该有一封激活邮件，其中包含指示你在之前所在的 Freenode 频道中输入类似`/msg NickServ VERIFY REGISTER nickname jeaxzxmgzqv`的指令。照做后，你应该会看到一条类似 -NickServ- nickname has now been verified 的消息。就这样，你已注册成功！点击左侧窗格中的 #ubuntu 频道返回到之前的位置。

![](img/f7cef0df22f9dba5a41777808c98eece_407_0.png)

Figure 20-11: Registering your IRC nickname

如果你收到的是 nickname is already registered 而不是关于激活邮件的消息，说明有人已经注册了你正在使用的昵称。在这种情况下，输入`/nick newname`，用新的昵称选择替换 newname，然后按 ENTER。你会看到一条消息说 You are now known as newname。理想情况下这次没有人使用相同的名字，所以尝试再次注册。

下次你进入 IRC 时，可以通过进入 freenode 频道，输入`/nick nickname`并按 ENTER 来取回你的已注册昵称。然后输入`/msg NickServ identify password`，再次按 ENTER。当然，用你自己的昵称和密码替换 nickname 和 password。

## IRC Etiquette

在 IRC 上就像在其他地方一样，有规则和社会规范需要遵守。不言而喻的是，你不应该刻意冒犯或骚扰任何人，就像在“现实世界”中一样。不过，还有一些更微妙的惯例你应该注意：

- Don't shout. Writing in ALL CAPITALS is the IRC equivalent of shouting all the time. There's a special circle of hell for shouters; this is pretty much everyone's pet peeve, and you're bound to get censured for doing it.
- Say things only once. Sometimes you won't get a reply for a while, so it can be tempting to keep repeating the same message until someone acknowledges it. Repeating yourself too many times is also considered annoying. Being patient is a necessary skill on IRC because people tend to dip in and
- Ubuntu 每周新闻（`https://wiki.ubuntu.com/UbuntuWeeklyNewsletter/`）：UWN 旨在每周概述社区动态，通常包括重要的 Ubuntu 新闻故事、开发者访谈以及软件近期变更的更新。它面向的是偏技术极客的读者群体。
- The Fridge（`http://fridge.ubuntu.com/`）：The Fridge 是社区成员张贴活动通知和更新的地方。有时也会发布访谈内容。
- Planet Ubuntu（`http://planet.ubuntu.com/`）：在这里你可以阅读 Ubuntu 开发者的个人博客。有些文章是技术性的，但如果你对前沿发展感兴趣，这里就是你要去的地方。

新闻和观点也会通过微博客服务传播。订阅 Twitter 上的 #ubuntu 话题标签，或加入 Identi.ca（`http://identi.ca/group/ubuntu/`）上的 Ubuntu 群组，即可参与推文、dent 或任何你想称呼它的互动。

## LoCo 团队与 LUG

到目前为止，整个 Ubuntu 社区的事情对你来说可能看起来有点，嗯，虚拟。难道不是吗？Ubuntu 是一个非常国际化的项目，在线沟通是完成事情最实际的方式。尽管如此，你仍有很多机会通过本地社区（LoCo）团队和 Linux 用户组（LUG）联系并结识你所在地区的其他 Ubuntu 用户。这些团体的成员通常拥有多样化的计算技能，因此它们是获取 Linux 帮助的好去处，还有其他方面的帮助。

LoCo 团队通常覆盖相当大的地理区域，通常以整个国家或州为单位。因此，它们线下见面的频率较低，不过许多 LoCo 团队全年都会安排与 Ubuntu 相关的活动，包括每次 Ubuntu 发布前后的“发布派对”。你可以在`https://wiki.ubuntu.com/LoCoTeamList/`找到 LoCo 团队列表。

LUG 比 LoCo 团队更为普及，并且更注重线下聚会。通常，LUG 会定期在当地社区中心（如果幸运的话，可能是一家酒吧）举行会议，并可能组织讲座或其他与 Linux 相关的活动。你可以在`http://www.linux.org/groups/`找到离你最近的 LUG。

## 贴纸和其他好东西

如果你有炫耀自己 Ubuntu 热爱的癖好，那你走运了！Ubuntu 友好型计算机制造商 system76 提供免费贴纸，它们非常适合遮盖你电脑机箱上某个角落可能藏着的难看 Windows 标志（见图 20-12）。要订购你的贴纸，请访问`http://www.system76.com/article_info.php?articles_id=9`，并将贴好邮票、写有地址的信封寄往该页面上的相应地址。没有会员徽章的俱乐部是不完整的，不是吗？

如果贴纸让你提不起兴趣，还可以通过 Canonical 商店（`http://shop.canonical.com/`）购买其他 Ubuntu 品牌的好东西。

![](img/f7cef0df22f9dba5a41777808c98eece_410_0.png)

## 参与进来

很多人喜欢成为 Ubuntu 社区的一员，并希望通过志愿服务来回馈社区。报告 bug 和使用 Brainstorm 是做出贡献的好方法，但这只是开始！
