Moving on, you can also use time conditions for sites. For example, if you want to allow access to the news sites in the evenings, you can set up a time category using this line:

```
acl freetime time MTWHFAS 18:00-23:59
```

This time, the category is called `freetime` and the condition is `time`, which means we need to specify what time the category should contain. The seven characters following that are the days of the week: `Monday`, `Tuesday`, `Wednesday`, `Thursday`, `Friday`, `Saturday`, and `Sunday`. Thursday and Saturday use capital *H* and *A* so that they do not clash with Tuesday and Sunday.

With the `freetime` category defined, you can change the `http_access` line to include it, like this:

```
http_access allow newssites freetime
```

For Squid to allow access now, it must match both conditions—the request must be for either `*.bbc.co.uk` or `slashdot.org`, and during the time specified. If either condition does not match, the line is not matched and Squid continues looking for other matching rules beneath it. The times you specify here are inclusive on both sides, which means users in the `freetime` category can surf from 18:00:00 until 23:59:59.

You can add as many rules as you like, although you should be careful to try to order them so that they make sense. Keep in mind that all conditions in a line must be matched for the line to be matched. Here is a more complex example:

+   * You want a category `newssites` that contains serious websites people need for their work.
+   * You want a category `playsites` that contains websites people do not need for their work.
+   * You want a category `worktime` that stretches from 09:00 to 18:00.
+   * You want a category `freetime` that stretches from 18:00 to 20:00, when the office closes.
+   * You want people to be able to access the news sites, but not the play sites, during working hours.
+   * You want people to be able to access both the news sites and the play sites during the free time hours.

To do that, you need the following rules:

```
acl newssites dstdomain *.bbc.co.uk, .slashdot.org
acl playsites dstdomain .tomshardware.com fedora.redhat.com
acl worktime time MTWHF 9:00-18:00
acl freetime time MTWHF 18:00-20:00
http_access allow newssites worktime
http_access allow newssites freetime
http_access allow playsites freetime
```