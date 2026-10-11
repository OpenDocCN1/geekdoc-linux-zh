# Command Mode

The mode that vi opens in is Command mode, sometimes also referred to as Normal mode. This is a realm in which every keystroke has a special meaning. Because so many different possibilities exist, this chapter takes a two-tiered approach. This section contains a series of tables that group together types of commands. Then, in the Immediate Solutions section I walk you through some of the more common tasks that vi users encounter. You should be used to some of the commands by now from reading solutions in other chapters that require use of vi, so the examples in this chapter are more complex than what you have already seen.

See one of the following tables for a listing of many of the commands available in vi, broken into the following categories:

+   • *Table 19.1*—Moving through your document in **vi**
+   • *Table 19.2*—Editing content in **vi**
+   • *Table 19.3*—Miscellaneous **vi** commands
+   • *Table 19.4*—Searching through your document in **vi**

> **NOTE:** In many cases, you can add a number before a **vi** command to tell the editor to do something in multiples. The **Multiples?** column in each of the tables indicates whether multiples is available for a particular command.

Table 19.1 Moving through a document in vi.

| Keystroke | Result | Multiples? |
| :--- | :--- | :--- |
| Ctrl+B | Jumps backward one screen | Yes |
| Ctrl+D | Jumps forward half a screen | Yes |
| Ctrl+E | Jumps backward half a screen | Yes |
| $ | Jumps forward to the end of the line | Yes |
| #% | Goes to the # percent point in the file | No |
| ' ' | Jumps backward to the beginning of the last line you jumped somewhere from | No |
| '[ | Jumps to the beginning of the first line in the section where you last edited material | No |
| ]' | Jumps to the beginning of the last line in the section where you last edited material | No |
| ( | Jumps backward one sentence | Yes |
| ) | Jumps forward one sentence | Yes |

*(continued)*