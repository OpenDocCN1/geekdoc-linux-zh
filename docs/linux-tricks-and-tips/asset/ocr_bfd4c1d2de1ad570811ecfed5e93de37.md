# # Executing Code from the Terminal

+   **STEP 5** Now enter: `exit()` to leave the command line Python session and return you back to the command prompt. Enter the folder where you saved the code from the previous tutorial and list the available files within; hopefully you should see the hello.py file.

![](bbox=[0.07, 0.21, 0.48, 0.38])

+   **STEP 6** From within the same folder as the code you're going to run, enter the following into the command line:
+   
+   `python3 hello.py`
+   
+   This will execute the code we created, which to remind you is:

```
```python
a="Python"
b="is"
c="cool!"
print(a, b, c)
```
```

![](bbox=[0.07, 0.55, 0.48, 0.67])

+   **STEP 7** Naturally, since this is Python 3 code, using the syntax and layout that's unique to Python 3, it only works when you use the `python3` command. If you like, try the same with Python 2 by entering:
+   
+   `python hello.py`

![](bbox=[0.07, 0.78, 0.48, 0.94])

+   **STEP 8** The result of running Python 3 code from the `python3` command line is quite obvious. Whilst it doesn't error out in any way, due to the differences between the way Python 3 handles the `Print` command over Python 2, the result isn't as we expected. Using Sublime for the moment, open the `hello.py` file.

![](bbox=[0.52, 0.22, 0.93, 0.37])

+   **STEP 9** Since Sublime Text isn't available for the Raspberry Pi, you're going to temporarily leave the Pi for the moment and use Sublime as an example that you don't necessarily need to use the Python IDLE. With the `hello.py` file open, alter it to include the following:
+   
+   `name = input("What is your name? ")`
+   `print("Hello,", name)`

![](bbox=[0.52, 0.51, 0.93, 0.67])

+   **STEP 10** Save the `hello.py` file and drop back to the command line. Now execute the newly saved code with:
+   
+   `python3 hello.py`
+   
+   The result will be the original Python is cool statement, together with the added `input` command asking you for your name, and displaying it in the command window.

![](bbox=[0.52, 0.81, 0.93, 0.94])