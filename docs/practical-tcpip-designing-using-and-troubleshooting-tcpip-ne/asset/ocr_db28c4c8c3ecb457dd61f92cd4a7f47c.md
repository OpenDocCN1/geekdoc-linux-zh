You can list the contents of the WINS server's database using menu **Mappings > Show Database** (Figure 19.6).

For a large network, the number of entries is correspondingly large, and WINS Manager's small display is hard to use. If you just need to look at one machine's entries, you can use the **Set Filter** button to restrict your view. Alternatively, you can use the program **winsdmp.exe** from the NT 4.0 Resource Kit. Figure 19.7 shows a partial **winsdmp** listing; the funny characters are the 16th-byte suffixes we mentioned in Module 19.2, which display oddly because they're outside the normal printable range.

```
```
Command Prompt

C:\>winsdmp 192.0.2.7
[2 owner(s) found]
[1] 192.0.2.12 (Highest ID = 2a7h)l
[Reading records in the range 0h - 7cfh ... 8 records found]

      192.0.2.12, "TEST-NTD    ","0,17,1,0,0,7,0,100165408,1,10.1.1.34,
      192.0.2.12, "WHI9000-NT  ","3,17,0,0,667,0,100165408,1,192.0.2.12,
      192.0.2.12, "WHI9000-NT  ","C0,17,0,0,668,0,100165408,1,192.0.2.12,
      192.0.2.12, "WHI9000-NT  ","0,17,0,0,669,0,100165408,1,192.0.2.12,
      192.0.2.12, "TEST-NTD    ","4E,17,0,0,670,0,100165408,1,192.0.2.12,
      192.0.2.12, "TEST-NTD    ","4B,17,0,0,671,0,100165408,1,192.0.2.12,
      192.0.2.12, "TEST-NTD    ","4C,17,2,0,0,672,0,100165408,1,192.0.2.12,
      192.0.2.12, "WHI9000-NT      ","BF,17,0,0,0,679,0,1001662503,1,192.0.2.12,
```
```

**Figure 19.7** A partial *winsdmp* listing

The Resource Kit contains another command-line tool, **winscl.exe**, that you can use to interrogate the server and control many aspects of its operation; see Web Appendix 25 for details. **winscl** is a horrible program to use, but:

+   - it lets you send very specific name queries to WINS servers, giving you more control than if you just *ping* the name
+   - the way it displays groups is clearer than WINS Manager's.

You can stop or start the WINS server from **Control Panel > Services**, or from the command line, using the **net** command:

```
```
net  start  wins
net  stop  wins
```
```

although you're unlikely ever to want to do this except when testing, or exploring how name resolution operates.