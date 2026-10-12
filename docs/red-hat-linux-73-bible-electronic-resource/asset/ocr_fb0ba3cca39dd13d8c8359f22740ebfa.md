```
keywords:               false
```

+   The keyartlimit parameter limits the maximum size of news articles for which keywords are added to the keyword database. The default is 100000, which represents about 100KB maximum size, as follows:

```
keyartlimit:             100000
```

+   The keylimit parameter sets the maximum amount of space that can be used to store keyword data. The default value is 512 bytes. If that limit is exceeded, further keyword data is discarded. Here is the default value:

```
keylimit:                512
```

+   The keymaxwords parameter indicates the maximum amount of keywords that can be used from any one article. The default value is 250 words. (Some words that are not significant, such as the or and, are not generated and will not be counted in reaching this maximum.)

```
keymaxwords:             250
```

# Posting parameters

Parameters in this section help define how programs that generate and accept postings behave. Many of these parameters relate particularly to how local postings are handled.

+   The addnnppostingdate parameter indicates whether or not to add the following header to local posts: NNTP-Posting-Date. This is on (true) by default, as follows:

```
addnnppostingdate:        true
```

+   The addnnppostinghost parameter indicates whether or not to add the following header to local posts: NNTP-Posting-Host. The information in this header is either the IP address or the fully-qualified domain name of the INN server. This is on (true) by default, as follows:

```
addnnppostinghost:        true
```

+   The checkincludedtext parameter restricts how much included text can appear in a news article that is posted from your server. Included text is text from an article the user is responding to (indicated by a > character) that is copied into the current article. By default, this parameter is set to false, so there is no restriction on included text. If you set it to true, however, less than half of the text in a message can contain include lines. Turning this parameter on can result in better performance by not allowing articles that simply repeat previously sent text. Here is an example of having this parameter turned on to restrict articles containing too much included text:

```
checkincludedtext:  true
```

+   The value of the complaints parameter can be set to define an e-mail address that is placed in the X-Complaints-To: line in articles that originate from your server.