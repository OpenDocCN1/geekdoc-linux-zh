If I want to see who's on the vax-plus mailing list, the output would look like this.

```
```text
>> who vax-plus
Members of list 'vax-plus':
User1@host.com
User2@hostl.com
User4@myhost.org
User5@yourhost.net
```
```

If I want to see what lists are available on Majordomo@the.vax.com, I send it the lists command:

```
```text
>> lists
Majordomo@the.vax...com serves the following lists:
```
```

row_h-i	Keeping old and new VAXers together. Announcements only.

test	Testing only. Don't.

tigerjokes	Jokes and amusement from [HOBBS]

unixtips	Unix Tip o' the Day from [HOBBS]

vax-plus	General discussions, musings, and rantings.

vp-digest	Digest version of vax-plus

weird	Flakes, wacos and weirdos and holders of SleazeFest.

If I wanted to find out which lists on this server I'm subscribed to, I'd send it the following command:

```
```text
>> which stripes@tigerlair.com
The string 'stripes@tigerlair.com' appears in the following
entries in lists served by Majordomo@the.vax...com:
```
```

List	Address

----	------

row_h-i	stripes@tigerlair.com

tigerjokes	stripes@tigerlair.com

unixtips	stripes@tigerlair.com

vax-plus	stripes@tigerlair.com

If I wanted to see the index of files available from the vax-plus mailing list, I would get an index of the files.

```
```text
>> index vax-plus
#### No files available for vax-plus.
```
```