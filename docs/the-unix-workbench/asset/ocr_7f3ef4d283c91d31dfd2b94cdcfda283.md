Journal

a-tale-of-two-cities.txt

Looks good! Another hidden use of the mv command is that you can use it to rename files and folders. The first argument is the path to the folder or file that you want to rename, and the second argument is a path with the new name for the file or folder. Let’s rename todo.txt so it includes today’s date:

```
mv todo.txt todo-2017-01-24.txt
ls
```

```
Code
Documents
Photos
Desktop
Music
echo-out.txt
todo-2017-01-24.txt
```

Looks like it worked nicely. Similar to the mv command, the cp command copies a file or folder from one location to another. As you can see cp is used exactly like mv when copying files, the file or folder you wish to copy is the first argument, followed by the path to the folder where you want the copy to be made:

```
cp echo-out.txt Desktop
ls
```