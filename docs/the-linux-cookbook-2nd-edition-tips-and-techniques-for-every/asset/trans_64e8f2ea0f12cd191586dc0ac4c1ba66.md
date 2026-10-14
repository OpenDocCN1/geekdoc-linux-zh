

3. 现在输入文本将其扩展为：
`Global expansion for "ww": Walla Walla, Washington RET`

现在，每当你在当前缓冲区中输入文本 "ww" 后跟一个空白字符或标点字符时，该文本将扩展为文本 "Walla Walla, Washington。"

要保存你已定义的 abbrevs 以便以后使用，请使用 `write-abbrev-file` 函数。这会将当前定义的所有 abbrevs 保存到一个文件中，你可以在未来的 Emacs 会话中读取该文件。 （你也可以在缓冲区中打开该文件并编辑 abbrevs。）

⇒ 要将你当前定义好的 abbrevs 保存到文件 "~/.abbrevs"，请输入：
`ALT-X write-abrev-file RET ~/.abbrevs RET`

然后，在未来的 Emacs 会话中，你可以使用 `read-abbrev-file` 函数为该会话定义这些 abbrevs。

⇒ 要从文件 "~/.abbrevs" 读取 abbrevs 并为当前会话定义它们，请输入：
`ALT-X read-abbrev-file RET ~/.abbrevs RET`

**NOTES:** Emacs 模式命令是切换式的。因此，要在缓冲区中关闭 `abbrev-mode`，只需再次输入 `ALT-X abbrev-mode RET`。如果你在该 Emacs 会话期间稍后在该缓冲区中打开 `abbrev-mode`，abbrevs 将被记住并再次展开。

## 10.1.6 在 Emacs 中录制和运行宏

*macro* 就像是一段按键序列的录制——当你运行宏时，Emacs 会执行该按键序列，就像你亲自输入了一样。

要开始录制宏，请输入 `CTRL-X (`。然后，你输入的所有内容都会被记录为宏，直到你通过输入 `CTRL-X )` 停止录制。录制宏后，你可以在 Emacs 会话期间的任何时间通过输入 `CTRL-X e` 播放它。你可以在前面加上 `universal-argument` 命令 `CTRL-U` 来指定播放次数。

⇒ 以下是一些使用方法。

- 要录制一个宏，将当前行的第一个单词大写（`ALT-C` 将光标右侧的单词大写），然后前进到下一行，请输入：
  `CTRL-X ( CTRL-A ALT-C`
  `CTRL-N CTRL-X )`

- 要播放该宏 20 次，请输入：
  CTRL-U 20 CTRL-X e

NOTES: 宏是 Emacs 工作方式的基础——事实上，Emacs 这个名字来源于 "Editing MACRos"，因为 1976 年的第一个 Emacs 版本实际上是为另一文本编辑器编写的一组这样的宏。

## 10.1.7 同时查看多个 Emacs 缓冲区

你可以将 Emacs 框架分成多个窗口，每个窗口显示自己的缓冲区。这对于同时查看多个缓冲区的不同部分很有用。当你有一个很长的缓冲区，想在编辑另一部分的同时查看其中一部分时也很方便——如果将框架分成两部分，你可以在一个窗口中移动到要查看的文本，在另一个窗口中编辑不同的部分。

使用 CTRL-X 2 将当前框架上下分成两个窗口，使用 CTRL-X 3 垂直分割它，使其左右并排。默认情况下，当前缓冲区显示在两个窗口中，但你可以随时更改任何窗口中显示的缓冲区。在 X 中，使用鼠标调整任一窗口的大小——在窗口的模式行上左键单击并拖动以调整该窗口的大小。

通过使用鼠标指针定位光标然后左键单击，或通过输入 CTRL-X o 来在不同窗口之间切换，后者会切换到另一个窗口。当你需要从长文件的一个部分反复剪切文本选择到另一个部分时，这非常方便：在一个窗口中剪切文本，在另一个窗口中将其粘贴到合适位置。当有许多选择需要剪切和粘贴时，这种方法可以节省时间。

使用 CTRL-X 1 删除多个窗口并使框架再次成为单个窗口。

## 10.2 使用 Vi

Nvi
DEB: nvi
RPM: nvi
WWW: http://www.bostic.com/vi/
WWW: http://vasc.ri.cmu.edu/old_help/Editors/Vi/

以下配方适用于 Vi 编辑器。它的名字发音为 "vye"，有时也读作 "vee-eye"，是 visual 的缩写；当它首次发明时，它是

