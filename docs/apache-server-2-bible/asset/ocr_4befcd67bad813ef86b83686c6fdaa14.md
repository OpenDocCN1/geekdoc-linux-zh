You should now be able to browse any Web site as if you had no proxy. You can double-check that Squid is working correctly by checking the log file `/usr/local/squid/logs/access.log` from the proxy server and making sure the Web site you were viewing is in there.

# Tweaking Squid to fit your needs

Now that you have Squid up and running, you can customize it to fit your needs. Ultimately, a tool such as Squid should be completely transparent to your users. This "invisibility" removes the users from the complexity of administration and enables them to browse the Web as if there were no Web proxy server. Although I do not detail how to do that here, you may refer to the Squid Frequently Asked Questions at `http://squid.nlanr.net/Squid/FAQ/FAQ.html`. Section 17 of this site details using Squid as a transparent proxy.

> This section shows you the basics to using Squid as a Web proxy. Squid has many features above and beyond those discus here. If you are interested in making Squid function beyond the basics, visit the Squid Web page at `http://squid.nlanr.net`.

# Setting rules for Squid

By default, Squid does not restrict your users from accessing any sites. You can define rules in your `squid.conf` file to set access control lists and to allow or deny visitors according to these lists; for example:

```
acl BadWords url_regex foo bar
```

By adding the preceding line, you have defined an ACL rule called `BadWords` that matches any URL containing the words `foo` or `bar`.

> This applies to `http://foo.deepwell.com/pictures` and `http://www.thekenneddycompound.com/ourbar.jpg` because they both contain words that are members of `BadWords`.

By adding the following:

```
http_access deny BadWords
```

to `squid.conf`, you block your users from accessing any URLs that match this rule.

> Almost every administrator who uses word-based ACLs has a story about not examining all the ways in which a word can be used. You should realize that if you ban your users from accessing sites containing the word “sex,” you are also banning them from accessing `www.buildersexchange.com` and any others that may fall into that category.

# Changing Squid’s cache memory settings

You can control the amount of Web pages that Squid keeps in the cache memory.