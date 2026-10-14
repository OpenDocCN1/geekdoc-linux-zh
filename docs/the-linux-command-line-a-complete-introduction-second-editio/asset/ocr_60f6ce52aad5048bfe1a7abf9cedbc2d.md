This is because `uniq` only removes duplicate lines that are adjacent to each other.

`uniq` has several options. Table 20-2 lists the common ones.

**Table 20-2:** Common `uniq` Options

| Option | Long option | Description |
|---|---|---|
| `-c` | `--count` | Output a list of duplicate lines preceded by the number of times the line occurs. |
| `-d` | `--repeated` | Output only repeated lines, rather than unique lines. |
| `-f n` | `--skip-fields=n` | Ignore n leading fields in each line. Fields are separated by whitespace as they are in sort; however, unlike sort, `uniq` has no option for setting an alternate field separator. |
| `-i` | `--ignore-case` | Ignore case during the line comparisons. |
| `-s n` | `--skip-chars=n` | Skip (ignore) the leading n characters of each line. |
| `-u` | `--unique` | Output only unique lines. Lines with duplicates are ignored. |

Here we see `uniq` used to report the number of duplicates found in our text file, using the `-c` option:

```
```text
[me@linuxbox ~]$ sort foo.txt | uniq -c
    2 a
    2 b
    2 c
```
```

# Slicing and Dicing