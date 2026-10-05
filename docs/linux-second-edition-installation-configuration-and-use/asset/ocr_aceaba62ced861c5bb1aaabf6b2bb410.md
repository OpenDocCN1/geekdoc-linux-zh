Many users employ the email program as a mini-database for archiving various pieces of text, news and even WWW pages. This is possible because many WWW and news browsers are capable of sending the current document as email. Although the email program has not been designed as a database (and therefore becomes slow when too many messages are stored in a folder), holding is in most cases so easy that these disadvantages are gladly accepted.

In principle, the email program decides how the individual email messages are combined and stored in a folder. Under Linux/Unix, all programs comply with the unwritten rule that all email messages in a folder are stored as a very long text file. This has not the considerable advantage that it is possible to continue using the existing email archive when changing email program. (At most, it needs to be moved to a different directory).

As expected, the Outlook email program, which is quite popular under Microsoft Windows, does not keep to this standard. Thus, it is not easily possible to use Outlook folders in a different email program.

# Searching for text in the email archive

The internal organization of email is fairly easy, but to find a message in them is somewhat more difficult. (An exception to this rule is Netscape, which provides a workable search function.) In such cases, the remedy is simply to apply the grep command to the email file.

The following command searches all 1998 sent-mail files for the text enclosed in double quotes. For each entry, the file name and the relevant line of text are displayed.

```
user$ grep "search text" /mail/send-mail-*98
```

The grep options -3 (three lines before and after the detected line) and -n (display line number) allow the search result to be displayed in more detail.

You can also load a whole email folder into a text editor and search it. However, make sure that you do not modify the text — otherwise the email program might get confused about the organization of the messages.

# Address books

The most laborious and error-prone step when writing an email message is inputting the address. The abbreviations are often hard to remember and typing errors have fatal consequences. However, the problem is not too dramatic, as when you are writing a reply to an email message (using REPLY), the address is inserted automatically.

Nevertheless, you may wish to write a new message, in which case it is nice to be able to take the address from an address list. All email programs support the management of address books. Addresses can be extracted from existing email messages to minimize typing effort (and the probability of errors).