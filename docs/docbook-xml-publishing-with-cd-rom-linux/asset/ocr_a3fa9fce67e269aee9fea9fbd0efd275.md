Word, and you can use DocBook to create a file and then pass it on editors or management types in Word format so that they don't have to figure out another program.

To create RTF output, use the following command, also shown in Figure 6.10.

```
sgmltools -b rtf book.sgml
```

# Converting LinuxDoc to DocBook

If you've inherited some LinuxDoc files to maintain, you might want to convert them to DocBook to make it easier on yourself and anyone else who will be working with them. It's always simpler to work with one standard format than two or more. Luckily, SGMLtools supports converting from LinuxDoc to DocBook.

To convert a LinuxDoc file to DocBook, use the same syntax as before, as shown in the Figure 6.11.

```
sgmltools -b l12db oldbook.sgml
```

![](bbox=[0.066, 0.511, 0.735, 0.933])

Figure 6.10 RTF output in StarOffice *.*.*