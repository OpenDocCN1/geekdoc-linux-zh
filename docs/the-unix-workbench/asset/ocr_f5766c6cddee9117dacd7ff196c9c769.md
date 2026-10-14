```
## 2017-01-02-hiking01.jpg
## 2017-01-02-hiking02.jpg
## 2017-02-10-hiking01.jpg
## 2017-02-10-hiking02.jpg
```

Only the files starting with “2017” are listed! The command ls 2017* literally means: list the files that start with “2017” followed by zero or more of any character. As you can imagine using wildcards is a powerful tool for working with groups of files that are similarly named.

Let’s walk through a few other examples of using the star wildcard. We could only list the photos starting with “2016”:

```
ls 2016*
```

```
## 2016-06-20-datasci01.png
## 2016-06-20-datasci02.png
## 2016-06-20-datasci03.png
## 2016-06-21-lab01.jpg
## 2016-06-21-lab02.jpg
```

We could list only the files with names ending in .jpg:

```
ls *.jpg
```