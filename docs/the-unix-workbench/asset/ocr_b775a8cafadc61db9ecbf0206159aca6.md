```
## 2016-06-21-lab01.jpg
## 2016-06-21-lab02.jpg
## 2017-01-02-hiking01.jpg
## 2017-01-02-hiking02.jpg
## 2017-02-10-hiking01.jpg
## 2017-02-10-hiking02.jpg
```

In the case above the file name can start with a sequence of zero or more of any character, but the file name must end in .jpg. Or we could also list only the first photos from each set of photos:

```
ls *01.*
```

```
## 2016-06-20-datasci01.png
## 2016-06-21-lab01.jpg
## 2017-01-02-hiking01.jpg
## 2017-02-10-hiking01.jpg
```

All of the files above have names that are composed of a sequence of characters, followed by the adjacent characters 01., followed by another sequence of characters. Notice that if I had entered ls *01* into the console every file would have been listed since 01 is a part of all of the file names in my Photos directory.

Let’s organize these photos by year. First let’s create one directory for each year of photos: