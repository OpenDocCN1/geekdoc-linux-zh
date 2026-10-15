```
enatsuex ttyaY May 9 13:41 bakasmg ttypq May 9 13:09 (age)
coxt ttyaZ May 9 13:35 dodsondt ttyps May 8 11:37 (age)
scfarley ttyAa May 9 13:36 md ttypv May 8 08:23 (kraft)
nancy ttyAb May 9 13:12 rothenba ttypw May 9 13:15 (trinetra)
rick ttyAc May 9 13:12 xuxiufan ttypy May 9 13:16 (ector)
fitzte ttyAd May 9 13:47 nashrm ttyq3 May 9 13:04 (pc115)
maluong ttyAe May 9 13:46 dls ttyq5 May 9 13:06 (dialup01)
af5 ttyAg May 9 09:12 myounce ttyq8 May 9 02:14 (limbo)
zjin ttyAh May 9 13:44 liyan ttyq9 May 9 13:11 (volt)
herbertl ttyAi May 9 13:29 daffnelr ttyqA May 9 13:36 (localhost)
ebranson ttyAj May 9 13:44 mm ttyqB May 9 10:32 (mm)
billiam ttyAk May 9 13:36 jlapham ttyqC May 9 12:46 (mac18)
linet2 ttyAm May 9 11:04 chuicc ttyqE May 9 13:38 (icarus)
--More-- _
```

Notice that the pr program not only made this a two-column listing but also added a page header that indicates the current date and page number.

2. The header still doesn’t contain any information about the command name, and that would really be helpful. Fortunately, I easily can add the header information I want by using pr:

Click here to view code image

```
$ who | pr -h "(output of the who command)" -2 | more
```

```
May 9 13:50 2015 (output of the who command) Page 1

root console May 6 18:02 ab ttypk May 9 07:57 (nova)
princess ttyaV May 9 13:44 dutch ttypl May 8 13:36 (dov)
tempus ttyaW May 9 13:43 malman ttypm May 9 13:07 (dov)
enatsuex ttyaY May 9 13:41 bakasmg ttypq May 9 13:09 (age)
coxt ttyaZ May 9 13:35 dodsondt ttyps May 8 11:37 (age)
scfarley ttyAa May 9 13:36 md ttypv May 8 08:23 (kraft)
nancy ttyAb May 9 13:12 rothenba ttypw May 9 13:15 (trinetra)
rick ttyAc May 9 13:12 xuxiufan ttypy May 9 13:16 (ector)
fitzte ttyAd May 9 13:47 dls ttyq5 May 9 13:06 (dialup01)
maluong ttyAe May 9 13:46 myounce ttyq8 May 9 02:14 (limbo)
maritanJ ttyAf May 9 13:49 liyan ttyq9 May 9 13:11 (volt)
af5 ttyAg May 9 09:12 daffnelr ttyqA May 9 13:36 (localhost)
zjin ttyAh May 9 13:48 mm ttyqB May 9 10:32 (mm)
herbertl ttyAi May 9 13:29 jlapham ttyqC May 9 12:46 (mac18)
ebranson ttyAj May 9 13:44 chuicc ttyqE May 9 13:38 (icarus)
--More-- _
```

That’s much better.

3. I might want to compare the contents of two different directories. The -1 flag to ls forces the ls program to list the output one filename per line, so I can create a couple of files in this format easily:

```
$ ls -1 src > src.listing
$ ls -1 /tmp > tmp.listing
```

These files look like this:

Click here to view code image

```
$ head src.listing tmp.listing
==> src.listing <==
calc-help
```