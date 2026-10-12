# Note

There are two entries for overchan, one for use with the Storage Manager API and one for use without it; uncomment only the one matching your setup.

Assuming you installed INN under the default path of /usr/local/news, the appropriate feed entries will look like the following.

# For traditional storage method:

```
overview!:*Tc,WO:/usr/local/news/bin/overchan

crosspost:*:Tc,Ap,WR:/usr/local/news/bin/crosspost

innfeed:\
!*\
:Tc,Wm*,S16384:/usr/local/news/bin/startinnfeed -y
```

# For CNFS or timehash storage method:

```
overview!:*Tc,Ao,WmR:/usr/local/news/bin/overchan

innfeed:\
!*\
:Tc,Wm*,S16384:/usr/local/news/bin/startinnfeed -y
```

If the server will not be supporting readers (a transit news server only), it's not necessary to run overchan. If you do that, however, and you're using CNFS or timehash, be sure to leave overview.ct1 empty so that INN doesn't generate overview information either. See the section "overview.ct1" later in the chapter.

Finally, you need to add entries for any actual sites to which you will be feeding articles. They will all have the same general format:

```
my-feed-site.domain.com/exclude.list\
:newsgroup.list\
:Tc:innfeed!
```

Set the feed name to the name of the remote site, and if the site uses a name other than its hostname for path headers, put that in the exclude list (if your exclude list is empty, leave out the "/" after the site name as well). The newsgroup list can be left empty if the default newsgroup pattern from your ME entry is sufficient. Otherwise, set the newsgroup pattern appropriately. The last line should not be modified.