```
touch small.txt
echo "abcdefghijklmnopqrstuvwxyz" >> small.txt
echo "ABCDEFGHIJKLMNOPQRSTUVWXYZ" >> small.txt
echo "0123456789" >> small.txt
echo "aa bb cc" >> small.txt
echo "rhythms" >> small.txt
echo "xyz" >> small.txt
echo "abc" >> small.txt
echo "tragedy + time = humor" >> small.txt
echo "http://www.jhsph.edu/" >> small.txt
echo "%%&--%%#--&%#" >> small.txt
```

In addition to quantifiers there are also regular expressions for describing sets of characters. The \w metacharacter corresponds to all “word” characters, the \d metacharacter corresponds to all “number” characters, and the \s metacharacter corresponds to all “space” characters. Let’s take a look at using each of these metacharacters on small.txt:

```
egrep "\w" small.txt
```

```
## abcdefghijklmnopqrstuvwxyz
## ABCDEFGHIJKLMNOPQRSTUVWXYZ
## 0123456789
## aa bb cc
## rhythms
## xyz
## abc
## tragedy + time = humor
## http://www.jhsph.edu/
```