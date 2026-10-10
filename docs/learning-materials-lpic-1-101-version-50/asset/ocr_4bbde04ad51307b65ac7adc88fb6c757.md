# ## Answers to Guided Exercises

+   1. What is the command to install a package named `package.deb` using dpkg?

Pass the `-i` parameter to dpkg:

```
```
# dpkg -i package.deb
```
```

+   2. Using `dpkg-query`, find which package contains a file named `7zr.1.gz`.

Add the `-S` parameter to `dpkg-query`:

```
```
# dpkg-query -S 7zr.1.gz
```
```

+   3. Can you remove a package called `unzip` from the system using `dpkg -r unzip` if the package `file-roller` depends on it? If not, what would be the correct way to do it?

No. `dpkg` will not resolve dependencies, and will not let you remove a package if another installed package depends on it. In this example, you could first remove `file-roller` (assuming nothing depends on it) and then remove `unzip`, or remove both at the same time with:

```
```
# dpkg -r unzip file-roller
```
```

+   4. How can you find out which package contains the file `/usr/bin/unrar` using the `apt-file` utility?

Use the `search` parameter followed by the path (or filename):

```
```
# apt-file search /usr/bin/unrar
```
```

+   5. Using `apt-cache`, what is the command to show information for the package `gimp`?

Use the `show` parameter followed by the package name:

```
```
# apt-cache show gimp
```
```