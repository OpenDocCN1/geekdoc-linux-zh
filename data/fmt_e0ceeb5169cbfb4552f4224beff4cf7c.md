
| ' | u | ú |
| ` | a | à |
| ` | e | è |
| ` | i | ì |
| ` | o | ò |
| ` | u | ù |
| ~ | a | ã |
| ~ | c | ç |
| ~ | d | d̃ |
| ~ | n | ñ |
| ~ | t | t̃ |
| ~ | u | ũ |
| ~ | < | << |
| ~ | > | >> |
| ~ | ! | ¡ |
| ~ | ? | ¿ |
| ^ | a | â |
| ^ | e | ê |
| ^ | i | î |
| ^ | o | ô |
| ^ | u | û |
| / | a | å |
| / | e | æ |
| / | o | ø |

⇒ 要在当前缓冲区点处写出文本 “Emacs ist spaß!”，输入：

`ALT-X iso-accents-mode RET`

*Emacs ist spaß!*

如果在缓冲区中启用了 `iso-accents-mode`，你想输入组成带重音字符的字面键组合，请键入前缀字符两次。

⇒ 要在 `iso-accents-mode` 打开的缓冲区中输入文本 “i o”（而不是重音字符 ó），输入：

`''o`

## METHOD #2

要在不进入 `iso-accents-mode` 的情况下在缓冲区中插入带重音字符和其他特殊语言字符，请使用 `⟨CTRL⟩-⟨X⟩ ⟨8⟩` 后跟特殊键组合，即重音前缀和字符，如前表所述。

非字母字符在此方法中不需要重音前缀。

⇒ 要在当前缓冲区点处写出文本 ‘¡Hasta Mañana!’，输入： `⟨CTRL⟩-⟨X⟩ ⟨8⟩ ⟨!⟩`Hasta Ma`⟨CTRL⟩-⟨X⟩ ⟨8⟩ ⟨-⟩`nana!

NOTES: 当缓冲区包含带重音字符时，它就不能再保存为纯 ASCII 文本，而必须保存为 ISO-8859-1 字符集中的文本（参见 Recipe 9.3.7 [Viewing a Character Set], page 228）。当你保存缓冲区时，Emacs 会通知你必须这样做。

最近，一系列国际化函数已添加到 GNU Emacs。它们使用的完整讨论超出了本书的范围；有关此主题的更多信息，请参阅 The GNU Emacs Manual 的“International Character Set Support”部分。

### 10.1.5 Making Abbreviations in Emacs

An abbrev is a word that is an abbreviation of a (usually) longer word or phrase. Abbrevs exist as a convenience to you—you can define abbrevs to expand to a long phrase that is inconvenient to you to type, or you can define a misspelling that you tend to make to expand to its correct spelling. Abbrevs only expand when you have `abbrev-mode` enabled.

⇒ 要打开 `abbrev-mode`，输入： `⟨ALT⟩-⟨X⟩ abbrev-mode ⟨RET⟩`

要定义一个 abbrev，输入你想要使用的 abbrev，然后输入 `⟨CTRL⟩-⟨X⟩ aig`。Emacs 将在 minibuffer 中提示你输入 abbrev 要扩展到的文本；输入该文本然后输入 `⟨RET⟩`。

- 要将 “ww” 定义为 ‘Walla Walla, Washington,’ 的 abbrev，请执行以下操作：
  1. 首先，输入 abbrev 本身：
     `ww`
  2. 接下来，指定此文本为 abbrev；输入： `⟨CTRL⟩-⟨X⟩ aig`
  3. 现在输入文本将其扩展为：
     `Global expansion for "ww": Walla Walla, Washington RET`

现在，每当你在当前缓冲区中输入文本 "ww" 后跟一个空白字符或标点字符时，该文本将扩展为文本 "Walla Walla, Washington。"

要保存你已定义的 abbrevs 以便以后使用，请使用 `write-abbrev-file` 函数。这会将当前定义的所有 abbrevs 保存到一个文件中，你可以在未来的 Emacs 会话中读取该文件。 （你也可以在缓冲区中打开该文件并编辑 abbrevs。）

⇒ 要将你当前定义好的 abbrevs 保存到文件 `"~/.abbrevs"`，请输入：
`ALT-X write-abrev-file RET ~/.abbrevs RET`

然后，在未来的 Emacs 会话中，你可以使用 `read-abbrev-file` 函数为该会话定义这些 abbrevs。

⇒ 要从文件 `"~/.abbrevs"` 读取 abbrevs 并为当前会话定义它们，请输入：
`ALT-X read-abbrev-file RET ~/.abbrevs RET`

**NOTES:** Emacs 模式命令是切换式的。因此，要在缓冲区中关闭 `abbrev-mode`，只需再次输入 `ALT-X abbrev-mode RET`。如果你在该 Emacs 会话期间稍后在该缓冲区中打开 `abbrev-mode`，abbrevs 将被记住并再次展开。

#### 10.1.6 在 Emacs 中录制和运行宏

*macro* 就像是一段按键序列的录制——当你运行宏时，Emacs 会执行该按键序列，就像你亲自输入了一样。

要开始录制宏，请输入 `CTRL-X (`。然后，你输入的所有内容都会被记录为宏，直到你通过输入 `CTRL-X )` 停止录制。录制宏后，你可以在 Emacs 会话期间的任何时间通过输入 `CTRL-X e` 播放它。你可以在前面加上 `universal-argument` 命令 `CTRL-U` 来指定播放次数。

⇒ 以下是一些使用方法。
- 要录制一个宏，将当前行的第一个单词大写（`ALT-C` 将光标右侧的单词大写），然后前进到下一行，请输入：
  ```
  CTRL-X ( CTRL-A ALT-C
  CTRL-N CTRL-X )
  ```
- 要播放该宏 20 次，请输入：
  `CTRL-U 20 CTRL-X e`

NOTES: 宏是 Emacs 工作方式的基础——事实上，Emacs 这个名字来源于 "Editing MACRos"，因为 1976 年的第一个 Emacs 版本实际上是为另一文本编辑器编写的一组这样的宏。

#### 10.1.7 同时查看多个 Emacs 缓冲区

你可以将 Emacs 框架分成多个窗口，每个窗口显示自己的缓冲区。这对于同时查看多个缓冲区的不同部分很有用。当你有一个很长的缓冲区，想在编辑另一部分的同时查看其中一部分时也很方便——如果将框架分成两部分，你可以在一个窗口中移动到要查看的文本，在另一个窗口中编辑不同的部分。

使用 `CTRL-X 2` 将当前框架上下分成两个窗口，使用 `CTRL-X 3` 垂直分割它，使其左右并排。默认情况下，当前缓冲区显示在两个窗口中，但你可以随时更改任何窗口中显示的缓冲区。在 X 中，使用鼠标调整任一窗口的大小——在窗口的模式行上左键单击并拖动以调整该窗口的大小。

通过使用鼠标指针定位光标然后左键单击，或通过输入 `CTRL-X o` 来在不同窗口之间切换，后者会切换到另一个窗口。当你需要从长文件的一个部分反复剪切文本选择到另一个部分时，这非常方便：在一个窗口中剪切文本，在另一个窗口中将其粘贴到合适位置。当有许多选择需要剪切和粘贴时，这种方法可以节省时间。

使用 `CTRL-X 1` 删除多个窗口并使框架再次成为单个窗口。

### 10.2 使用 Vi

Nvi

DEB: `nvi`

RPM: `nvi`

WWW: http://www.bostic.com/vi/

WWW: http://vasc.ri.cmu.edu/old_help/Editors/Vi/

以下配方适用于 Vi 编辑器。它的名字发音为 "vye"，有时也读作 "vee-eye"，是 visual 的缩写；当它首次发明时，它是

是早期能够在整个屏幕上可视化显示文本以进行交互式编辑的文本编辑器之一（当时其他交互式编辑器通常逐行显示文件）。

与 Emacs 类似，Vi 也有许多变体；其中较为流行的几个是 Vim 和 Elvis，它们都是更新的实现，比原始 Vi 具有更多功能。本节将假设使用 Nvi，即为 BSD 实现的原始 Vi 的新实现，目前在大多数 Linux 系统上都能找到。

#### 10.2.1 熟悉 Vi

与 Emacs 一样，熟悉 Vi 的方法是启动它，并尝试一些基本编辑。

你可以通过在 X 中从窗口管理器提供的菜单中选择它，或在 shell 提示符下输入其名称（小写字母）来启动 Vi。提供一个文件名以开始编辑文件。

⇒ 这里有两种方法可以做到这一点。
- 要在 shell 提示符下启动 Vi，输入：
  ```
  $ vi ⟨RET⟩
  ```
