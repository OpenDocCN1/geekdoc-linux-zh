```
return False
key = self.key(movie.title, movie.year)
bisect.insort_left(self.__movies, [key, movie])
self.__movieFromId[id(movie)] = movie
self.__dirty = True
return True
```

The first if statement ensures that we don't add the same movie twice. We use the key() method to generate a suitable order key, and then use the bisect module's insert\_left() function to insert the two-element [key, movie] list into the \_\_movies list. This is very fast because the bisect module uses the binary chop algorithm. We also make sure that the \_\_movieFromId dictionary is up-to-date, and set the container to be dirty.

```
def key(self, title, year):
    text = unicode(title).lower()
    if text.startswith("a "):
        text = text[2:]
    elif text.startswith("an "):
        text = text[3:]
    elif text.startswith("the "):
        text = text[4:]
    parts = text.split(", ", 1)
    if parts[0].isdigit():
        text = "%08d % " % int(parts[0])
        if len(parts) > 1:
            text += parts[1]
    return u"%s\t%d" % (text.replace(" ", ", ", 1), year)
```

This method generates a key string suitable for ordering our movie data. We do not guarantee key uniqueness (although it would not be difficult to do), because the ordered data structure is a list in which duplicate keys are not a problem. The code is English-specific, eliminating the definite and indefinite articles from movie titles. If the movie's title begins with a number, we pad the number with leading zeros so that, for example, "20" will come before "100" We do not need to pad the year, because years are always exactly four digits. All the other data is stored using PyQt data types, but we have chosen to use unicode for the key strings.

```
def delete(self, movie):
    if id(movie) not in self.__movieFromId:
        return False
    key = self.key(movie.title, movie.year)
    i = bisect.bisect_left(self.__movies, [key, movie])
    del self.__movies[i]
    del self.__movieFromId[id(movie)]
    self.__dirty = True
    return True
```