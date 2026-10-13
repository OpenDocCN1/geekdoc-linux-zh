If more than one file is specified, the output includes the contents of both files concatenated together. For example, the following command outputs the contents of the files fruits and users:

```
$ cat fruits users
```

```
Fruit  Price/lbs  Quantity
Banana $0.89 100
Peach $0.79 65
Kiwi $1.50 22
Pineapple $1.29 35
Apple $0.99 78

ranga
vathsa
amma
```

# Numbering Lines

The -n option of cat will number each line of output. It can be used as follows:

```
$ cat -n fruits
```

This produces the output

```
1  Fruit  Price/lbs  Quantity
2  Banana $0.89 100
3  Peach $0.79 65
4  Kiwi $1.50 22
5  Pineapple $1.29 35
6  Apple $0.99 78
7
```

From this output, you can see that the last line in this file is blank. We can ask cat to skip numbering blank lines using the -b option as follows:

```
$ cat -b fruits
```

Now the output resembles the following:

```
1  Fruit  Price/lbs  Quantity
2  Banana $0.89 100
3  Peach $0.79 65
4  Kiwi $1.50 22
5  Pineapple $1.29 35
6  Apple $0.99 78
```

The blank line is still present in the output, but it is not numbered. If the blank line occurs in the middle of a file, it is printed but not numbered:

```
$ cat -b hosts
1  127.0.0.1  localhost  loopback

2  128.32.43.52  soda.berkeley.edu  soda
```