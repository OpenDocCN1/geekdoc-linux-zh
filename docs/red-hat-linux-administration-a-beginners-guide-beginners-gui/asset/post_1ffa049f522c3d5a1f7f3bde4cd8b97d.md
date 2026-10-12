
## Compiling Macros into a Configuration File

Once you have all of your macros put into a `.mc` file, you are ready to convert it into a complete configuration file that Sendmail can understand. The process is wonderfully straightforward. Invoke the m4 processor, passing it the name of your macro file, and redirect the output to the name of the resulting file that you want to use.

```bash
[root@mail mail]# m4 myconfig.mc > sendmail.cf
```

And that's it. The file `sendmail.cf` has been created and is ready to use. If you're really curious, you might peek at the resulting `sendmail.cf` and see how it compares with the macro file you started with.

## Beyond the Primary Configuration File

Reading through the features that Sendmail offers us, we saw that there are many features that enable and disable the usage of additional configuration files. Some of these files are very straightforward and are explained in a sentence or two in the previous section. But there are two files in particular that are nontrivial: the **aliases** file and the **access** database file. In this section, we examine their formats and learn how to write our own.

### The aliases File

Sendmail’s mail **aliases** file is one of Sendmail’s most powerful features. It allows you to create mailing lists, give users alternative e-mail aliases, and even pipe e-mail directly to external applications. Though some newer systems prefer to move the **aliases** file to /etc/mail/aliases, Red Hat has chosen to leave it in its traditional location at /etc/aliases.

The format of the **aliases** file is reasonably straightforward. All comment lines begin with a pound symbol (#), and the remainder of the line is free-form. Lines may also be blank to help define logical blocks.

Each alias must begin with the alias’s name, followed immediately by a colon. The remainder of the line is what Sendmail will expand that address to be. The content of the line can be one of six things: another alias, a list of aliases, another user, a list of users, a file, or an external application. Aliases and usernames can be intermixed. Any aliases referenced on the right side of the colon must have been previously defined.

Assume the **domain** **example.com** has the users **boss**, **alice**, **ask**, **wally**, **bob**, **mordac**, and **dilbert**. Let’s look at a few examples and see what some of these aliases can be set up to do.

- We want a simple alias for **boss**. Since she is the CEO, we will set up an alias as follows:
  ```
  ceo: boss
  ```
  Now any mail sent to **ceo@example.com** will transparently be sent to **boss**.

- We want to create an alias for three of our departments: **engineering**, **mis**, and **management**. We can create the aliases as follows:
  ```
  engineering: dilbert, wally
  mis: mordac, bob
  management: bob, alice, ceo
  ```
  Any mail sent to **management@example.com** will automatically be forwarded to the users **alice**, **bob**, and **ceo**. The **ceo** address will get expanded to **boss**.

- We want to create the alias **everybody** so that any mail sent to it will automatically be forwarded to all of the departments. We can do that with the following alias:
  ```
  everybody: engineering, mis, management
  ```
  E-mail sent to **everybody@domain.com** will be expanded to **engineering**, **mis**, and **management**. Each of these aliases will expand to their respective users, with the management alias having one more expansion to convert **ceo** to **boss**.

- If we want all of the mail sent to a particular address to be copied to a file, we simply begin the right side of an alias with a forward slash character (`/`), indicating that the rest of the line is a filename. So if we want messages sent to log@example.com to be placed into a file called /tmp/log, we would set an alias, like so:
  ```
  Log: /tmp/log
  ```

- If we want to pipe all of the e-mail sent to a particular alias to an external program, we can do so through this file. Assume that the external program is /etc/smcrsh /external_program.
  ```
  abuse: "| /etc/smcrsh/external_program"
  ```

![](img/ec2066d370d3af1a767664d36aa7ddfe_426_0.png)

> You will need to be sure to place your binaries in the correct directory so that smcrsh knows they are there. Under a standard Red Hat installation, this would be the directory /etc/smcrsh.

Once you have finished creating the aliases file, you will need to use the newaliases command to convert the file into a database format that Sendmail can quickly read. To do so, simply type

```bash
[root@mail /etc]# newaliases
```

### Spam Control: The access Database

Sendmail allows you to use the /etc/mail/access file to list special actions for particular domain names, host names, IP addresses, and users. This feature is especially interesting because it unifies all of Sendmail’s spam-control mechanisms into a single configuration file.

The format of the file is simple: lines that begin with a pound symbol (#) are comments, blank lines are allowed, and the rest of the lines contain the actual configuration information.

The default features of using the access_db allow you to list either the host name, domain name, IP address, or e-mail address, and specify whether you want a specific action on e-mail originating from there. The actions are listed in Table 13-3.

Let’s look at a few examples that illustrate the features listed in Table 13-3:

- To reject all messages from **annoying-web-site.com**, your entry would be
  ```text
  annoying-web-site.com REJECT
  ```

- To discard all messages from **badperson@badpeople.com**, you would use
  ```text
  badperson@badpeople.com DISCARD
  ```

- To relay all messages from the 138.23.0.0 network, you would use
  ```
  138.23                                     RELAY
  ```

- To reject all messages from spamathon.com with the SMTP message "$50 No Spam Here.", you would use
  ```
  spamathon.com                              550 No Spam Here.
  ```

- You can also blacklist an individual address:
  ```
  spamsender@badpeople.com                    550 Been blacklisted.
  ```

We can put all of these examples together into a single file:

```
#
# /etc/mail/access
# Rules for accepting/denying mail from various sites.
#
annoying-web-site.com                        REJECT
badperson@badpeople.com                       DISCARD
138.23                                        RELAY
spamathon.com                                 550 No Spam Here.
spamsender@badpeople.com                      550 Been blacklisted...
```

| Action | Description |
|---|---|
| OK | Accepts the message even if there are other rules that would otherwise reject it. For example, if you enable the feature to deny messages from domain names that cannot be resolved to an IP address, you can specify a specific exception domain using the OK action. |
| RELAY | Unless explicitly turned on, the default Sendmail configuration does not relay messages for other domains. This action overrides that rule for a specific domain. |
| REJECT | Refuses all messages from this site/person. This will cause a brief message to be sent back to the sender informing him or her that the message was rejected. |
| DISCARD | Discards the message entirely. No message is sent back to the sender. For all he/she knows, the message was accepted. |
| SMTP-code message | SMTP-code must be a valid SMTP code as specified in RFC 821. message can be any text you want returned along with SMTP-code. |

Table 13-3 *access.db* Features
