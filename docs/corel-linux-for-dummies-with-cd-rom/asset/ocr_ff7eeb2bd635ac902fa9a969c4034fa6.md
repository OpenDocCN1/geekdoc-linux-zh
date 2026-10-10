3. **Type `cd /home/elmz/data` to go to the directory where Corel Linux found your letters.**

4. **Find your addresses by searching for a specific string, such as by a name in your addresses list.**

For instance, if you type

```
```bash
grep -i "Zijijeman" *.txt
```
```

Corel Linux displays the name of the file(s) found, such as

```
```
Important.txt
```
```

Now that you’ve found the files, it’s time to copy them to a safe place. You have a choice of copying the files to your Windows partition or to a floppy disk.

To copy the files to your Windows partition, type

```
```bash
cp /home/elmz/data/Letter*.wpd /disks/c/data
cp /home/elmz/data/Important.txt /disks/c/data
```
```

If you instead want to copy the files to a floppy disk, you must mount the floppy drive first:

```
```bash
mount -t msdos /dev/fd0 /mnt/floppy
```
```

Then you type

```
```bash
cp /home/elmz/data/Letter*.wpd /mnt/floppy
```
```

That wasn’t too hard, was it?

# Moving some system files

Here’s a real-life example of using command mode that I encountered while writing this book. In demonstrating how you can create a desktop link to your files, I accidentally copied my X11R6 graphical system files to the desktop instead of linking to them! My Corel Linux graphical lights immediately went out as I was unceremoniously kicked into back-screened command mode.

The tragedy of moved system files can happen only when you’re logged in as root.

![](bbox=[0.04, 0.8, 0.14, 0.9])