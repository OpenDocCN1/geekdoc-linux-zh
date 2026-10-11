You can include a subject line to your e-mail by using the -s switch, following it with the text of the subject. Insert the switch and the subject between the mail and the destination address at the command prompt, as shown in the following example:

```
mail -s "Promotions" bob@mycomputer < memo1
```

The -s switch tells the mail utility to use Promotions as the subject of the e-mail. Always include the subject within double quotation marks.

# ### Inserting multiple addresses

The mail utility can send the same e-mail to many destination addresses and copy the e-mail to many other addresses. You can achieve this task by inserting the additional addresses next to each other, separating each address with a space.

Say, for example, that I want to send the e-mail to my co-workers Sandy, Joanne, and Anne, in addition to good old Bob. The following example shows how I do it:

```
mail bob@mycomputer sandy@mycomputer joanne@mycomputer anne@mycomputer < memo1
```

The mail utility treats each address as a destination address, which means that these addresses all appear in the To portion of the e-mail. You can also insert multiple addresses to send copies of the e-mail by placing the addresses after the -c switch. You must separate each address with a space.

Say I want to send one e-mail to Bob and copy the e-mail to Sandy, Joanne, and Anne. The following example shows how I do it:

```
mail bob@mycomputer -c sandy@mycomputer joanne@mycomputer anne@mycomputer < memo1
```

# ### Inserting a copy address

A copy address is another e-mail address that receives a copy of the e-mail, along with the destination address of the e-mail. Everyone who receives the e-mail also sees the copy addresses.

Say, for example, that I send the promotion memo to Bob and his boss, Mary, and Mary’s boss, Mark. Bob sees Mary’s and Mark’s e-mail addresses as "cc" on the e-mail. Mary also sees that her boss is receiving the e-mail, too, just as Mark knows that Mary is receiving the same e-mail.

Be careful in copying anyone on an e-mail, because you may not want everyone who receives the e-mail to know about all the other people who receive