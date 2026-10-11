
## Your First Code

  Essentially, you’ve already written your first piece of code with the `print("Hello everyone!")` function from the previous tutorial. However, let’s expand that and look at entering your code and playing around with some other Python examples.

### Playing with Python

  With most languages, computer or human, it’s all about remembering and applying the right words to the right situation. You’re not born knowing these words, so you need to learn them.

- **STEP 1**
  If you’ve closed Python 3 IDLE, reopen it in whichever operating system version you prefer. In the Shell, enter the familiar following:
  ```python
  print("Hello")
  ```
  ![](img/4aefeb2d095f688b34af6207870c5f39_13_0.png)

- **STEP 2**
  Just as predicted, the word Hello appears in the Shell as blue text, indicating output from a string. It’s fairly straightforward and doesn’t require too much explanation. Now try:
  ```python
  print("2+2")
  ```
  ![](img/4aefeb2d095f688b34af6207870c5f39_13_2.png)

- **STEP 3**
  You can see that instead of the number 4, the output is the `2+2` you asked to be printed to the screen. The quotation marks are defining what’s being outputted to the IDLE Shell; to print the total of 2+2 you need to remove the quotes:
  ```python
  print(2+2)
  ```
  ![](img/4aefeb2d095f688b34af6207870c5f39_13_1.png)

- **STEP 4**
  You can continue as such, printing `2+2`, `464+2343` and so on to the Shell. An easier way is to use a variable, which is something we will cover in more depth later. For now, enter:
  ```python
  a=2
  b=2
  ```
  ![](img/4aefeb2d095f688b34af6207870c5f39_13_3.png)

- **STEP 5**
  What you have done here is assign the letters a and b two values: 2 and 2. These are now variables, which can be called upon by Python to output, add, subtract, divide and so on for as long as their numbers stay the same. Try this:
  ```python
  print(a)
  print(b)
  ```
  ![](img/4aefeb2d095f688b34af6207870c5f39_14_0.png)

- **STEP 6**
  The output of the last step displays the current values of both a and b individually, as you've asked them to be printed separately. If you want to add them up, you can use the following:
  ```python
  print(a+b)
  ```
  This code simply takes the values of a and b, adds them together and outputs the result.
  ![](img/4aefeb2d095f688b34af6207870c5f39_14_1.png)

- **STEP 7**
  You can play around with different kinds of variables and the Print function. For example, you could assign variables for someone's name:
  ```python
  name="David"
  print(name)
  ```
  ![](img/4aefeb2d095f688b34af6207870c5f39_14_2.png)

- **STEP 8**
  Now let's add a surname:
  ```python
  surname="Hayward"
  print(surname)
  ```
  You now have two variables containing a first name and a surname and you can print them independently.
  ![](img/4aefeb2d095f688b34af6207870c5f39_14_3.png)

- **STEP 9**
  If we were to apply the same routine as before, using the + symbol, the name wouldn't appear correctly in the output in the Shell. Try it:
  ```python
  print(name+surname)
  ```
  You need a space between the two, defining them as two separate values and not something you mathematically play around with.
  ![](img/4aefeb2d095f688b34af6207870c5f39_14_4.png)

- **STEP 10**
  In Python 3 you can separate the two variables with a space using a comma:
  ```python
  print(name, surname)
  ```
  Alternatively, you can add the space yourself:
  ```python
  print(name+" "+surname)
  ```
  The use of the comma is much neater, as you can see. Congratulations, you've just taken your first steps into the wide world of Python.
  ![](img/4aefeb2d095f688b34af6207870c5f39_14_5.png)

## Saving and Executing Your Code

  While working in the IDLE Shell is perfectly fine for small code snippets, it’s not designed for entering longer program listings. In this section you’re going to be introduced to the IDLE Editor, where you will be working from now on.

### Editing Code

  You will eventually reach a point where you have to move on from inputting single lines of code into the Shell. Instead, the IDLE Editor will allow you to save and execute your Python code.

- **STEP 1**
  First, open the Python IDLE Shell and when it’s up, click on File > New File. This will open a new window with Untitled as its name. This is the Python IDLE Editor and within it you can enter the code needed to create your future programs.

- **STEP 2**
  The IDLE Editor is, for all intents and purposes, a simple text editor with Python features, colour coding and so on, much in the same vein as Sublime. You enter code as you would within the Shell, so taking an example from the previous tutorial, enter:
  ```python
  print("Hello everyone!")
  ```

- **STEP 3**
  You can see that the same colour coding is in place in the IDLE Editor as it is in the Shell, enabling you to better understand what’s going on with your code. However, to execute the code you need to first save it. Press F5 and you get a Save... Check box open.

- **STEP 4**
  Click on the OK button in the Save box and select a destination where you’ll save all your Python code. The destination can be a dedicated folder called Python or you can just dump it wherever you like. Remember to keep a tidy drive though, to help you out in the future.

  ![](img/4aefeb2d095f688b34af6207870c5f39_15_0.png)
  ![](img/4aefeb2d095f688b34af6207870c5f39_15_1.png)
  ![](img/4aefeb2d095f688b34af6207870c5f39_15_2.png)
  ![](img/4aefeb2d095f688b34af6207870c5f39_15_3.png)

- **STEP 5**
  Enter a name for your code, 'print hello' for example, and click on the Save button. Once the Python code is saved it’s executed and the output will be detailed in the IDLE Shell. In this case, the words ‘Hello everyone!’.
  ![](img/4aefeb2d095f688b34af6207870c5f39_16_0.png)

- **STEP 6**
  This is how the vast majority of your Python code will be conducted. Enter it into the Editor, hit F5, save the code and look at the output in the Shell. Sometimes things will differ, depending on whether you’ve requested a separate window, but essentially that’s the process. It’s the process we will use throughout this book, unless otherwise stated.
  ![](img/4aefeb2d095f688b34af6207870c5f39_16_2.png)

- **STEP 7**
  If you open the file location of the saved Python code, you can see that it ends in a .py extension. This is the default Python file name. Any code you create will be whatever.py and any code downloaded from the many Internet Python resource sites will be .py. Just ensure that the code is written for Python 3.
  ![](img/4aefeb2d095f688b34af6207870c5f39_16_4.png)

- **STEP 8**
  Let’s extend the code and enter a few examples from the previous tutorial:
  ```python
  a=2
  b=2
  name="David"
  surname="Hayward"
  print(name, surname)
  print (a+b)
  ```
  If you press F5 now you’ll be asked to save the file, again, as it’s been modified from before.
  ![](img/4aefeb2d095f688b34af6207870c5f39_16_1.png)

- **STEP 9**
  If you click the OK button, the file will be overwritten with the new code entries, and executed, with the output in the Shell. It’s not a problem with just these few lines but if you were to edit a larger file, overwriting can become an issue. Instead, use File > Save As from within the Editor to create a backup.
  ![](img/4aefeb2d095f688b34af6207870c5f39_16_3.png)

- **STEP 10**
  Now create a new file. Close the Editor, and open a new instance (File > New File from the Shell). Enter the following and save it as hello.py.
  ```python
  a="Python"
  b="is"
  c="cool!"
  print(a, b, c)
  ```
  You will use this code in the next tutorial.
  ![](img/4aefeb2d095f688b34af6207870c5f39_16_5.png)

## Python on Linux

### Executing Code from the Terminal

  Although we’re working from the GUI IDLE throughout this book, it’s worth taking a look at Python’s command line handling. We already know there’s a command line version of Python but it’s also used to execute code.

### Command the Code

  Using the code we created in the previous tutorial, the one we named hello.py, let’s see how you can run code that was made in the GUI at the command line level.

- **STEP 1**
  Python, in Linux, comes with two possible ways of executing code via the command line. One of the ways is with Python 2, whilst the other uses the Python 3 libraries and so on. First though, drop into the command line or Terminal on your operating system.
  ![](img/4aefeb2d095f688b34af6207870c5f39_17_0.png)

- **STEP 2**
  Just as before, we’re using a Raspberry Pi: Windows users will need to click the Start button and search for CMD, then click the Command Line returned search; and macOS users can get access to their command line by clicking Go > Utilities > Terminal.
  ![](img/4aefeb2d095f688b34af6207870c5f39_17_1.png)

- **STEP 3**
  Now you’re at the command line we can start Python. For Python 3 you need to enter the command **python3** and press Enter. This will put you into the command line version of the Shell, with the familiar three right-facing arrows as the cursor (>>>).
  ![](img/4aefeb2d095f688b34af6207870c5f39_17_2.png)

- **STEP 4**
  From here you’re able to enter the code you’ve looked at previously, such as:
  ```python
  a=2
  print(a)
  ```
  You can see that it works exactly the same.
  ![](img/4aefeb2d095f688b34af6207870c5f39_17_3.png)
