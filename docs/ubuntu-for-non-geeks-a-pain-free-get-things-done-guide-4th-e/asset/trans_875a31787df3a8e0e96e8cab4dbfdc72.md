

## 17B-2：获取和解压 Schnapsen

安装了 Java 运行时环境后，你需要运行一个 Java 应用程序才能看到它发挥作用。你将要安装的应用程序是我自从进入 Linux 世界以来一直在寻找的，一款 2 张牌的奥地利纸牌游戏，名为 Schnapsen，如图 17-17 所示。

开始之前，你需要下载并解压 Schnapsen。以下是需要执行的操作：

- 1. 打开你的网页浏览器，并前往 *http://projects.hagru.at/tiger/en/.*
- 2. 在该页面上，点击左侧框架中的 **Schnapsen** 链接。
- 3. 在右侧框架中，点击 **Schnapsen.zip**。

![](img/f7cef0df22f9dba5a41777808c98eece_356_0.png)

*图 17-17：奥地利纸牌游戏 Schnapsen 的 Java 版本*

- 4. 在随后出现的 Opening Schnapsen_1.00.zip 窗口中，接受默认的 *Open with Archive Manager*，点击 **OK**。
- 5. 当 Archive Manager 窗口出现时，点击 **Extract** 按钮，这将打开提取窗口。
- 6. 在该窗口中，点击 **Create Folder** 按钮，并在你的主文件夹内创建一个名为 *Schnapsen* 的文件夹。
- 7. 在该窗口中点击 **Extract** 按钮，并在提取过程完成后退出 Archive Manager。

## 17B-3：运行和英文化 Schnapsen

现在 Schnapsen 已在你的主文件夹中，是时候运行它了。打开一个新的终端窗口，然后执行以下操作：

- 1. 通过输入 cd Schnapsen 并按下 ENTER 进入新的 Schnapsen 文件夹。
- 2. 输入 java -jar Schnapsen.jar（请确保在 java 和 jar 之间留一个空格，并在 Schnapsen 开头使用大写 S），然后按下 ENTER。Schnapsen 很快就会出现，之后你就可以开始游戏了……如果你会德语的话。
- 3. 要将界面切换为英语，请前往 Einstellungen 菜单，并选择 Sprache ▸ Englisch。
- 4. 如果你不熟悉德语的纸牌花色和牌面（在本游戏中称为 Traditional），你可以将它们切换为你可能熟悉的法国花色（方块、红心、黑桃和梅花），方法是前往 Settings 菜单，并在 Cards' set 和 Trump sign 菜单中都选择 French（图 17-18）。

如果你想知道你在上一行做了什么，这里是解释：命令字符串的第一部分 java 调用 Java 运行时环境；其后的 -jar 标志告诉 Java 你将要运行一个 JAR 文件，这就是 Java 脚本的名称；最后一部分是你将要运行的实际文件 Schnapsen.jar。（将来，如果你选择运行其他基于 Java 的应用程序，只需遵循相同的模式：java -jar application_name.jar。）

![](img/f7cef0df22f9dba5a41777808c98eece_357_0.png)

图 17-18：在 Schnapsen 中将德语花色和牌面切换为法语

你现在可以开始游戏了。帮助菜单中有一些基本规则，但你也可以在 http://www.pagat.com/ 更深入地学习 Schnapsen（以及世界上任何其他纸牌游戏）的规则。祝你玩得开心！

## 在线游戏

谈到安装游戏，很容易忘记还有许多游戏根本不需要安装。众多网站允许你免费在线玩游戏，只要安装了适当的浏览器插件即可。（请参阅第 62 页的“Multimedia Plug-Ins”以获取安装插件的帮助。）例如，查看 http://www.popcap.com/ 和 http://gametrick.net/，那里有一些很棒的在线消磨时间游戏。你也可以在 Facebook 或其他社交网络网站上玩任何游戏，例如 Farmville 和 Mafia Wars，而无需离开你的 Ubuntu 桌面。

## 搜索更多游戏

还有很多我没有介绍的 Ubuntu 优秀游戏，但可以放心，它们都在那里。有些以 DEB 文件形式提供，可以像你在第 6 章中安装 Skype 的方式一样安装。一个很好的例子是 SDL Hana，即日本花牌游戏 Hanafuda 的 Linux 版本（图 17-19），可从 http://savannah.nongnu.org/pr/sdlhana/ 获取。

![](img/f7cef0df22f9dba5a41777808c98eece_358_0.png)

*图 17-19：SDL Hana*

Ubuntu 软件中心中还有更多游戏可供使用：我一些老式最爱包括塞尔维亚的 Pac Man 克隆版 Njam；以及捷克迷宫游戏 Fish Fillets NG，在该游戏中你需要引导两条鱼穿过各种笨拙但非常漂亮的水下地点。

