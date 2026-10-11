Looking at this more verbose output, it’s easy to see that there’s a great deal going on. Some of it is not directly pertinent to checking the `%files` list, however. For example, the output extending from the first line to the line reading `* Package: cdplayer` reflects processing that takes place during actual package building and can be ignored.

Following that section is the actual `%files` list check. In this section, every file named in the `%files` list is checked to make sure it exists. The phrase ADDING: again reflects RPM’s package building roots. When using the -b1 option, however, RPM is simply making sure the files exist on the build system. If the -timecheck option (described a bit later, in section 12.1.14) is present, the checks required by that option are performed here, as well.

After the list check, the MD5 checksums of each file are calculated and displayed. While this information is vital during actual package building, it is not used when using the -bi option.

Finally, RPM determines which shared libraries the listed files require. In this case, there are only two: `libC.so.5` and `libuseres.so.2.0`. While not strictly a part of the list-checking process, displaying shared library dependencies can be quite helpful at this point. It can point our possible problems, such as assuming that the target systems have a certain library installed when, in fact, they do not.

So far, we’ve only seen what happens when the `%files` list is correct. Let’s see what happens where the list has problems. In this example, we’ve added a bogus file to the package’s `%files` list:

```
# rpm -b1 cdplayer-1.0.spec
Package: cdplayer
File List Check: cdplayer-1.0-1
File not found: /usr/local/bin/bogus
Build failed.
```

Reflecting more of its package building roots, `rpm -b1` says that the build failed. But the bottom line is that there is no such file as `/usr/bin/bogus`. In this example, we made the name obviously wrong, but in a more real-world setting, the name will more likely be a misspelling in the `%files` list. Okay, let’s correct the `%files` list and try again:

```
# rpm -b1 cdplayer-1.0.spec
Package: cdplayer
File List Check: cdplayer-1.0-1
File not found: /usr/local/bin/cdplay
Build failed.
```

Another error! In this case the file is spelled correctly, but it is not on the build system, even though it should be. Perhaps it was deleted accidentally. In any case, let’s rebuild the software and try again:

```
# rpm -bi cdplayer-1.0.spec
* Package: cdplayer
Executing: %prep
```