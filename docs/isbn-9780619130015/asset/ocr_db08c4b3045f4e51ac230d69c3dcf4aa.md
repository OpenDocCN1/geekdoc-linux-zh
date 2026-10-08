![](bbox=[0.2, 0.1, 0.8, 0.45])

Figure 7-16: Output of updated os_choice script

In the next exercise, you modify a while loop so it uses the test command.

**To modify a while loop to use the test command:**

+   1.  Recall the script named colors, which you wrote in Chapter 6. It repeatedly asks the user to guess its favorite color, until the user guesses the color red.
```bash
echo -n "Try to guess my favorite color "
read guess
while [ "$guess" != "red" ]; do
    echo "No, not that one. Try again. "; read guess
done
```
2.  Load the file into vi or Emacs.
3.  Change the line that reads:
```bash
while [ "$guess" != "red" ]; do
```
So it reads:
```bash
while test $guess != "red" ; do
```
4.  Save the file and exit the editor.