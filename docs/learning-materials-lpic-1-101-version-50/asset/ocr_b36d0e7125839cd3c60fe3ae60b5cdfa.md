# ## Guided Exercises

+   1. It’s convenient to save the execution date of actions performed by automated scripts. Command `date +%Y-%m-%d` shows the current date in *year-month-day* format. How can the output of such a command be stored in a shell variable called `TODAY` using command substitution?

+   2. Using command `echo`, how can the contents of variable `TODAY` be sent to the standard input of command `sed s/-/./g`?

+   3. How could the output of command `date +%Y-%m-%d` be used as a Here string to command `sed s/-/./g`?

+   4. Command `convert image.jpeg -resize 25% small/image.jpeg` creates a smaller version of `image.jpeg` and places the resulting image in a likewise named file inside subdirectory `small`. Using `xargs`, how is it possible to perform the same command for every image listed in file `filelist.txt`?