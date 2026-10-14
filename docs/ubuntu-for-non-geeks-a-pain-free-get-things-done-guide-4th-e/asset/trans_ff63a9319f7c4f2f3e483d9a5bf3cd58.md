

![](img/f7cef0df22f9dba5a41777808c98eece_154_0.png)

Figure 7-21: Choosing where to save the backup files in Déjà Dup

> NOTE 如果你想把备份文件放到 CD 或 DVD 上，你必须先将它们保存到某个文件夹中，然后再使用本章前面提到的刻录软件将该文件夹复制到光盘上。

点击 Forward，你会看到 Figure 7-22 中的屏幕。你的第一个任务是决定要备份什么内容，因此查看标有 Include files in folders 的列表，目前其中应该只有你的 Home 文件夹。这对大多数人来说是相当合理的选择，因为你所有的文件都应该在 Home 文件夹中。你可以使用列表右侧的按钮随意添加和删除其他项目。

![](img/f7cef0df22f9dba5a41777808c98eece_154_1.png)

Figure 7-22: Selecting which files you want to backup

该屏幕上还有另一个列表，标为 Except files in folders。你可以用它来定义任何你不想备份的文件或文件夹。举例来说，如果你想备份 Home 文件夹中的所有内容，除了你的图片——也许你的备份磁盘没有足够的空间容纳所有图片。你只需要确保 Home 文件夹在 Include files in folders 列表中，而 Pictures 文件夹在 Except files in folders 列表中即可。

当你选择好要保留和要忽略的内容后，再次点击 Forward 进入摘要页面。检查一切看起来是否 hunky-dory，然后点击 Backup 开始备份。如果你选择了加密备份，你将被要求输入密码，输入后点击 Continue。

务必妥善保管该密码；否则，日后你将无法恢复备份文件！随后会进行一阵文件复制，如果你要备份的文件很多，可能需要花费一些时间。完成后，点击 Close，并安全移除你的备份磁盘（或你使用的其他介质）。

就这样……暂时如此。但请记住，如果不定期备份，备份就毫无意义，因为如果出现问题，你只能恢复较旧的文件，而无法恢复更新的文件。我大约每月备份一次，但我应该比这更频繁一些。这并不是什么大麻烦；当你下次使用 Déjà Dup 时，它会记住上次备份的所有设置。如果你想做不同的设置，点击主窗口中的 Edit ▸ Preferences，然后在那里更改选项。你还会找到自动备份的选项：打开 Preferences 窗口，勾选 Automatically backup on a regular schedule 设置，然后选择你希望备份发生的频率。点击 Close，Déjà Dup 应该会处理剩下的事情。

> NOTE Canonical，也就是 Ubuntu 背后的公司，现在提供了一项名为 Ubuntu One 的在线备份服务。有关该服务的更多信息，请访问 https://one.ubuntu.com/。

## Recovering from a Backup

理想情况下你永远不需要恢复备份，但如果需要，这里有一个快速指南：

- 1. 找到你的备份磁盘，将其连接到计算机，并启动 Déjà Dup。
- 2. 选择 Edit ▸ Preferences，并确保该磁盘被选为 Backup location。点击 Close 返回主屏幕。
- 3. 点击 Restore，如果你对备份进行了加密，请输入你选择的密码。
- 4. 系统会要求你选择要恢复的备份。选择看起来正确的那个（通常是最新的），然后点击 Forward。
- 5. 如果你希望文件被放回原来的位置，选择 Restore files to original locations。否则，你可以选择一个文件夹来恢复它们。再次点击 Forward。
- 6. 浏览摘要以确保一切看起来正常，然后点击 Apply 恢复你的文件。你可能需要重新输入加密密码，如果被要求，请继续操作。
- 7. 恢复完成后点击 Close，并检查文件是否已正确放回。

一切应该都恢复正常了。呼！

