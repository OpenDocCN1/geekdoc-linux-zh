Why is it necessary to do all this checking? When would it be useful? Keep in mind that the %files list must be generated manually. By using the -bi option, the following steps are all that's necessary to create a %files list:

+   - Writing the %files list
+   - Using the -bi option to check the %files list
+   - Making any necessary changes to the %files list

It may take more than one iteration through these steps, but eventually the list check will pass. Using the -bi option to check the %files list is certainly better than starting a two-hour package build, only to find out at the very end that the list contains a misspelled filename.

Here's an example of the -bi option in action:

```
```
# rpm -bi cdp Player -1.0 .spec
Package: cdp Player
File List Check: cdp Player -1.0 -1
Finding dependencies ...
Requires (2): libc.so.5 libncurses.so.2.0
#```

```

It's hard to see exactly what RPM is doing from the output, but if we add -vv, we can get a bit more information:

```
```
# rpm -bi -vv cdp Player -1.0 .spec
D: Switched to BASE package
D: Source(0) = sunsite .unc .edu:/pub/Linux/apps/sound/cds/cdp Player -1.0 .tgz
D: Switching to part: 12
D: fileFile =
D: Switched to package: (null)
D: Switching to part: 2
D: fileFile =
D: Switching to part: 3
D: fileFile =
D: Switching to part: 4
D: fileFile =
D: Switching to part: 10
D: fileFile =
D: Switched to package: (null)
* Package: cdp Player
File List Check: cdp Player -1.0 -1
D: ADDING: /usr/doc/cdp Player -1.0 -1
D: ADDING: /usr/doc/cdp Player -1.0 -1/README
D: ADDING: /usr/local/bin/cdp
ADDING: /usr/local/bin/cdpay
D: ADDING: /usr/local/man/man1/cdp.1
D: md5(/usr/doc/cdp Player -1.0 -1/README) = 2c149b2f1a4ad e5418131a19b242601c
D: md5(/usr/local/bin/cdp) = 0fa2a72f8121c75f0d1c52f456798d6
D: md5(/usr/local/bin/cdpplay) = da1d8cd98f00b204e9800998ecf8427e
D: md5(/usr/local/man/man1/cdp.1) = b32cc867ae50e2bfdad67b00004adf a
Finding dependencies ...
D: Adding require: libncurses.so.2.0
D: Adding require: libc.so.5
Requires (2): libc.so.5 libncurses.so.2.0
#```

```