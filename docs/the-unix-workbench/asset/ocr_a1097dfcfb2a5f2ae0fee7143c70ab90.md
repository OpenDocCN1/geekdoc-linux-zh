```
```bash
egrep "North|South" states.txt
```
```

```
```text
## North Carolina
## North Dakota
## South Carolina
## South Dakota
```
```

In the example above we’re searching for lines of text that contain the words “North” or “South”. You can also use multiple pipe characters to, for example, search for lines that contain the words for all of the cardinal directions:

```
```bash
egrep "North|South|East|West" states.txt
```
```

```
```text
## North Carolina
## North Dakota
## South Carolina
## South Dakota
## West Virginia
```
```

Just two more notes on grep: you can display the line number that a match occurs on using the -n flag:

```
```bash
egrep -n "t$" states.txt
```
```

```
```text
## 7:Connecticut
## 45:Vermont
```
```

And you can also grep multiple files at once by providing multiple file arguments: