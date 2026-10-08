# Case Logic

The **case logic** structure simplifies the selection of a match when you have a list of choices. It allows your program to perform one of many actions, depending upon the value of a variable. Note the use of two semicolons ( ;; ) that terminate the action(s) taken after the case matches to the test.

+   **To demonstrate case logic:**
1. Use the vi or Emacs editor to create the manycolors shell script.
2. Type these lines into the file:

   ```bash
   echo -n "Enter your favorite color: "; read color
   case $color in
    "blue")   echo "As in My Blue Heaven.";;
    "yellow") echo "As in the Yellow Sunset.";;
    "red")    echo "As in Red Rover, Red Rover.";;
    "orange") echo "Autumn has shades of Orange.";;
    *         ) echo "Sorry, I do not know that color.";;
   esac
   ```
3. Save the file and exit the editor.
4. Give the file execute permission, and test it. You see output similar to that shown in Figure 6-8.

![](bbox=[0.22, 0.56, 0.78, 0.9])

Figure 6-8: Output of manycolors script