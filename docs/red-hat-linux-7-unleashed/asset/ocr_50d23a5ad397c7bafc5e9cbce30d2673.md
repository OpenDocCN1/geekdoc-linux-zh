you can test your configuration file `test.cf` by typing

```
```
$ /usr/sbin/sendmail -t<est.cf -bt < addr.test
rewrite: rulest 3 input: joe
rewrite: rulest 3 returns: joe
[etc.]
```
```

You also might want to follow one or more addresses through the complete rewriting process. For example, if an address resolves to the `smtp` mailer and that mailer specifies `R=21`, you can test recipient address rewriting by using `3,2,21,4 test_address`.

If the `sendmail.cf` appears to work correctly so far, you're ready to move on to sending some real letters. You can do so by using a command like the following:

```
```
$ /usr/sbin/sendmail -v -oO/tmp -t<est.cf < /dev/null
```
```

The `-v` option tells sendmail to be verbose so you can see what's happening. Depending on whether the delivery is local or remote, you can see something as simple as `joe... Sent` or an entire SMTP dialog. The `-o` sets an option that overrides what is in the `sendmail.cf` file. You can also use `-O` for long options.

The `-oO/tmp` tells sendmail to use `/tmp` as its queue directory. Using this option is necessary because sendmail drops its superuser permissions when run with the `-C` option and can't write queue files into the normal mail queue directory. Because you are using the `-C` and `-oO` options, sendmail also includes the following warning headers in the letter to help alert the recipient of possible mail forgery:

```
```
X-Authentication-Warning: gonzo.gov: Processed from queue /tmp
X-Authentication-Warning: gonzo.gov: Processed by joe with -C svr.cf
```
```

sendmail also inserts the header `Apparently-to:` because, although you specified a recipient on the command line, none was listed in the body of the letter. In this case, the letter's body was taken from the empty file `/dev/null`, so no `To:` header was available. If you do your testing as the superuser, you can skip the `-oO` argument and sendmail won't insert the warning headers. You can avoid the `Apparently-to:` header by creating a file like

```
```
To: recipient

testing
```
```

and using it as input instead of `/dev/null`.

The recipient should be you, so you can inspect the headers of the letter for correctness. In particular, return address lines must include an `FQDN` (Fully Qualified Domain Name) for SMTP mail. That is, a header such as `From: joe@gonzo` is incorrect because it doesn't include the domain part of the name, but a header such as `From: joe@gonzo.gov` is fine.