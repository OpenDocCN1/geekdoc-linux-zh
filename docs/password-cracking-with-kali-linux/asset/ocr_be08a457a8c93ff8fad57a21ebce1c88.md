The **combinator3** command is similar to **combinator**, but it focuses on generating more complex wordlist combinations by combining three input files. This can be especially useful for creating hybrid wordlists with increased variation.

Basic usage:

```
```
>       combinator3  [OPTIONS]  [INPUT_FILES]  >
  [OUTPUT_FILE]
```
```

For instance, to combine three wordlists, **dictionary1.txt**, **dictionary2.txt**, and **dictionary3.txt**, you would run:

```
```
  combinator3       dictionary1.txt      dictionary2.txt
  dictionary3.txt > combined_wordlist.txt
```
```

> **WARNING:** *Combinator created massive output files, Combinator3 generates ever LARGER files! I always watch my hard drive free space and hit "CTRL-C" to stop the generation if the files get too large.*

Depending on your specific needs, you can further customize the generated wordlists using Hashcat Utils' commands. For example, you can remove duplicates, sort the lists, apply rules, or use other utilities to refine your wordlist before using it with Hashcat for password cracking.

See the tool Wiki page for more information:

[https://hashcat.net/wiki/doku.php?id=hashcat_utils](https://hashcat.net/wiki/doku.php?id=hashcat_utils)