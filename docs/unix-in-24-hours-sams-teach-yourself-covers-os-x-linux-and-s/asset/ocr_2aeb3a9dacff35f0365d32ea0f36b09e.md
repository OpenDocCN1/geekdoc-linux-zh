1. The −x flag sorts across, listing the output in columns, or [row-first order](#) (where entries are sorted across, then down):

[Click here to view code image](#)

```
```text
% ls -a
.		.elm		.plan		Global.Software
..		.forward		.pnewsexpert	Interactive.Unix
.Pnews.header	.ircmod		.rnlast		Mail
.accinfo		.login		.rnlock		News
.article		.logout		.rnsoft		Src
.cshrc		.newsrc		.sig		bin
.delgroups		.oldnewsrc	.tin		history.usenet.Z

% ls -x -a
.		..		.Pnews.header	.accinfo
.article		.cshrc		.delgroups	.elm
.forward		.ircmod		.login		.logout
.newsrc		.oldnewsrc	.plan		.pnewsexpert
.rnlast		.rnlock		.rnsoft		.sig
.tin		Global.Software	Interactive.Unix	Mail
News		Src		bin		history.usenet.Z
```
```

2. Even more ways exist to sort files in ls. If you want to sort by most recently accessed to least recently accessed, you use the −t flag:

[Click here to view code image](#)

```
```text
% ls -a -t
./		../		.rnlock		.cshrc
.newsrc		News/		.rnlast		.sig
.oldnewsrc	.tin/		.rnsoft		.plan
.article		.ircmod		Interactive.Unix	Mail/
.elm/		.delgroups	.accinfo*	.Pnews.header*
.forward	.login		Src/		.pnewsexpert
history.usenet.Z	bin/		Global.Software	.logout
```
```

From this output, you can see that the most recently accessed files are .newsrc and .oldnewsrc and that it’s been quite a while since .logout was touched. Try using the −t flag on your system to see which files you’ve been accessing and which you haven’t.

3. So far, you know three different approaches to sorting files within the ls command: column-first order, row-first order, and most recently accessed-first order. But more options exist in ls than just these three. For example, the −r flag reverses any sorting order:

[Click here to view code image](#)

```
```text
% ls
Global.Software	Mail/		Src/		history.usenet.Z
Interactive.Unix	News/		bin/
% ls -r
history.usenet.Z	Src/		Mail/		Global.Software
bin/			News/		Interactive.Unix
```
```

4. Things can become confusing when you combine some of these flags. Try to list the contents of the directory that is one level above the current directory, sorted so the most recently accessed file is last in the list. At the same time, you want to know which items are directories and the size of each file. Use this: