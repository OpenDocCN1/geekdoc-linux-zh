
so that other news servers know not to forward the message to your server again. You can override the server parameter by setting the NNTPSERVER environment variable. Here is an example of a server parameter:

```
server:            news.hansonhistory.com
```

## News feed parameters

This set of parameters relates to how INN allocates resources to handle news feeds.

- To limit how long an article can be stored on your server, set the `artcutoff` parameter. By default, it is set to 10 days. Articles older than that are dropped. Here’s an example of the `artcutoff` parameter with a cutoff date of 14 days:

```
artcutoff:             14
```

- The `bindaddress` parameter sets which interface (IP address) the INN server listens on. The default is to listen on all network interfaces on the computer. Setting `bindaddress` to `All` also results in INN listening on all interfaces.

- The `hiscachesize` parameter can be used to set the amount of memory to make available (in kilobytes) to store message IDs. Storing these incoming messages can speed up history lookup. The default is `0` (no memory allocated) as follows:

```
hiscachesize:         0
```

- The `ignorenewsgroups` parameter can be used to control routing of newsgroup creation control messages. By default, this feature is off (`false`) as follows:

```
ignorenewsgroups:     false
```

- If the `immediatecancel` parameter is set to `true`, it can be used to immediately cancel articles (and not just set them in cache to be cancelled). This option is only available for `timecaf` storage methods. By default, the feature is off as follows:

```
immediatecancel:     false
```

- The `linecountfuzz` parameter rejects messages where the line count doesn’t match the value of the `Lines` header. The default is zero (`0`), which turns `linecountfuzz` off. Setting `linecountfuzz` to a number allows messages that differ up to the number of lines you set. In this example, messages whose line count differs more than five lines is rejected:

```
linecountfuzz         5
```

- With the `maxartsize` parameter, you can limit the size of the articles that are accepted by your news server. By default, this value is 1,000,000 bytes. To make the value half that size, you could set the parameter as follows:

```
maxartsize:		500000
```

- Use the `maxconnections` parameter to limit the number of incoming NNTP connections that are allowed from your server at the same time. NNTP connections, which enable users to read articles from and post articles to your news server, are handled by the `nnrpd` daemon. Limiting NNTP connections is one way to reduce demand on your server, but it can also prevent people from using it effectively. By default, `maxconnections` is set to 50. To set it to 40, use the following line:

```
maxconnections:		40
```

- You can use the `pathalias` parameter to prepend a name to the front of the `pathhost` value that appears on a news article's `Path:` line. No value is required.

- Control messages are used by Usenet to indicate when newsgroups should be added or removed. To prevent malicious users from faking control messages, INN administrators can now use PGP verification to verify the source of control messages. (Cancel messages are not verified.) The `pgpverify` parameter, which can be used to turn on this feature is off by default (false). Here is the default setting:

```
pgpverify:		false
```

- The `port` parameter lets you indicate which TCP/IP port to listen on. The default is 119, which is the standard news port.

```
port:			119
```

- By setting `refusecycercancels` to true, you can automatically refuse any article that has a message ID that begins with `<cancel`. This is one method, though an inefficient one, of refusing cancelled spam messages. This is off by default:

```
refusecycercancels:	false
```

- The `remembertrash` parameter lets your INN server keep a record of rejected articles so that further copies of messages it has received can be refused before they are sent. This is on by default, as follows:

```
remembertrash:		true
```

- The `sourceaddress` parameter sets which interface (IP address) the INN server binds to for outgoing traffic. The default is for the INN server to choose which interface to use from the available interfaces. Setting `sourceaddress` to all also results in INN listening on all interfaces.

- The `usecontrolchan` parameter lets you choose to handle non-cancel control messages with an external program.

There are also several other parameters that let you control news feeds. The `verifycancels` parameter lets you verify that a cancel message came from the same person that originated the post. The `wanttrash` parameter, if `true`, causes messages posted to unknown newsgroups to be sorted into the junk newsgroup. The `wipcheck` parameter sets a time limit (5 seconds by default) in which the server waits to receive a promised article from a news server peer before accepting the article from another news server. The `wipexpire` parameter sets how long (10 seconds by default) to keep a message ID for an article that was offered but not yet sent.

## Article storage parameters

Use storage-related parameters to set how newsgroup messages are stored on your hard disk.

- The `cnfscheckfudgesize` parameter causes the size of CNFS cycbuffs articles to be checked against the value plus the value of the `maxartsize` parameter. If the value is larger, the CNFS cycbuff is assumed to be corrupt. This parameter is off by default, based on the following value:

```
cnfscheckfudgesize: 0
```

- If the `enableoverview` parameter is `true` (default), overview data is written out for articles. When this parameter is `true`, the `ovmimethod` parameter must be set as well (as described earlier). Here is an example of the default `enableoverview` parameter:

```
enableoverview: true
```

- As the `groupbaseexpiry` parameter is set to `true`, expiration of newsgroup messages is done based on newsgroup name. If you change it to `false`, expiration is done based on the storage method class being used. Here is how the parameter is set by default:

```
groupbaseexpiry: true
```

- The `mergetogroups` parameter can be set to `true` if you want to file articles posted to `.to*` groups to pseudonewsgroups "to". If `true`, this parameter requires that the `to` newsgroup exist in the `active` file to allow INN to start. This feature is off (`false`) by default:

```
mergetogroups: false
```

- The `overcachesize` parameter sets the number of cache slots that are set aside to hold open overview files. INN will store and open overview files just in case articles are received for those newsgroups. This parameter is used only if `enableoverview` is `true` and `ovmimethod` is defined as `tradindexed`. By default, `overcachesize` is set to 15, as shown following:

```
overcachesize: 15
```

- The `ovgroupat` parameter can be used to limit overview information stored by the INN server. With the value set to `true`, overview information is only stored for newsgroups that match a comma-separated list of expressions (in wildmat format). This option is not set by default.

- To have the INN server store articles based on newsgroup name in the Xref header, the `storeonxref` parameter should be *true* (it is *false* by default). If this value is *false*, newsgroup articles are stored by newsgroup name in the Newsgroups header.

```
storeonxref:      false
```

- The `useoverchan` parameter can be used to turn on a feature where overview data are stored internally using the `libstorage` function. If *false*, which it is by default, the INN server will handle creation of overview data on its own. Here is how `useoverchan` is set by default:

```
useoverchan:      false
```

- You can turn on the `wireformat` parameter, if you are using the `tradspool` storage method, to write articles in wire format. With wire format, messages are stored with a `\r\n` ending each line and periods at the beginning of lines doubled. Articles formatted in this way require no conversion. The INN server can operate more efficiently with `wireformat` set to *true*. By default, the value is *false* as indicated below:

```
wireformat:       false
```

- The `xrefslave` parameter indicates that the INN server should be a slave to another server. In this arrangement, each INN server should have the same article numbering so that the two servers could be used interchangeably. If this value is set to *true*, you must set the host name of the other server using the `nnrpdposthost` parameter (described later). By default, this value is *false* as shown below:

```
xrefslave:        false
```

### Reading parameters

This set of parameters is used to validate newsreaders and features related to the newsreaders.

- If the `allownewnews` parameter is set to *true*, your users can request the NEWNEWS feature from their newsreaders. The NEWNEWS feature enables a user of a newsreader to request all articles that were posted or received for a particular newsgroup since a particular date. By default, this value is on (*true*), as recommended by the Network News Transfer Protocol RFC (RFC977). However, overuse of this feature can result in serious performance problems for the server. If you want to turn off NEWNEWS, set the value of the `allownewnews` parameter to *false*, as follows:

```
allownewnews:  false
```

- With the `articlemmap` parameter on, articles can be mapped into memory using the `mmap` function. By default, this parameter is off (*false*) and articles are read into memory before going to the newsreader.
