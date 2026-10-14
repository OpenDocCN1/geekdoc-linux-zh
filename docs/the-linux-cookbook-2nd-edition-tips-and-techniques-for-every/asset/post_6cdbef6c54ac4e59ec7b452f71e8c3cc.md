
⇒ To add to the CRON schedule any new entries that are in the file crontab, type:
    $ crontab crontab RET

NOTES: The name of the command, crontab, is the same as the file it uses, crontab.

## 27.5 Using Contact Managers

Loosely put, a contact manager is a piece of software that helps you keep track of information about people you may need to contact in the future. In the past, people often called the physical embodiment of these things a "rolodex," which incidentally is a trademarked brand name for the Cadillac of such contact managers, the circular Rolodex that sat atop the desk of every successful 20th century businessman. I hear that many people use them even today.

There are many contact manager programs available; the following recipes show two of the best and easiest methods of managing contact information with Linux.

### 27.5.1 Keeping a Free-Form Address List

The simplest way to keep names and addresses in Linux is to keep them in a text file as a free-form address list; to find an entry, use the search capabilities of tools like grep, less, and Emacs.

This method is useful when you need to keep track of name and address information for many parties, but you don't always keep the same kind of information for each—maybe sometimes a name and phone number, sometimes just a mailing address, sometimes a name and email address. With a free-form address list, each entry contains whatever information you have in the format you want. Separate the entries with a delimiter line of your preference. I happen to use "###," but you can use whatever characters you're comfortable with—just make it a combination that won't appear in the text for any of the entries themselves.

“fields”; you can even cut and paste text into it from email, the Web, or other windows (see Recipe 10.3 [Manipulating Selections of Text], page 253).

```
Mary Smith
14 Elm St
Centerville, New York

###

Susan Jones – 602 555 1803
(don't call after eight)

###

Prof. Jenkins, 25 College St, Uptown, New York
555-2011 jenkins@example.edu
```

![](img/be7f02611e5cefde1a18c788fede22f7_580_0.png)

There are several ways to find text in such a file. Suppose, for example, you want to contact your friend Susan, and you need her telephone number.

⇒ To output the line in the file containing the text “susan,” regardless of case, type:

```
$ grep -i susan rolo ⏎
Susan Jones – 602 555 1803
$
```

This works nicely when the information you need is on the same line as the information you search for—here, the name Susan is on the same line as the telephone number; however, the output did not show the warning that appears on the next line in the file. And what about when the term you search for and the information you need are on adjacent lines?

Use the -C option with grep to output several lines of context before and after matched lines.

⇒ To output the several lines around the line matching the text “Jenkins,” type:

```
```shell
$ grep -C Jenkins rolo RET

Prof. Jenkins, 25 College St, Uptown, New York
(914) 555-2011 jenkins@example.edu
$
```
```

Another way to search such a file is to open it as a buffer in Emacs and use any of the Emacs searches. The Emacs incremental-search function, CTRL-S, is very useful for such files—even for very large ones. If you do such a search on a large file, and the first result doesn’t turn up the right record, just keep typing CTRL-S until the right one appears. If you type the letters to search for in all lowercase, Emacs matches those letters regardless of case.

⇒ Here are two ways to use this.

- To search through the current buffer in Emacs for the first entry containing the text “New York,” regardless of case, type:
  
  `CTRL-S new york`
- To search for the next entry containing the text “New York,” regardless of case, type:
  
  `CTRL-S`

You can repeat this keystroke as many times as you wish to show all entries in the entire buffer with the text “New York” in them. Once you reach the end of the buffer, type CTRL-S again to loop around to the beginning of the buffer and continue the search from there. (The minibuffer will tell you when you’ve reached the end of the buffer, and will remind you to type this if you want to loop the search.)

**NOTES:** It’s also useful to peruse and search through these kinds of files with less—see Recipe 14.11 [Searching the Text You’re Pursing], page 354.

### 27.5.2 Keeping a Contact Manager Database

```
```text
BBdb
  DEB: bbdb
  RPM: bbdb
  WWW: http://bbdb.sourceforge.net/
```
```
