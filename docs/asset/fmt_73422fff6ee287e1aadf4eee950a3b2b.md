
```
//File: Invoke.java
import java.lang.reflect.*;

class Invoke {
public static void main( String [] args ) {
try {
Class c = Class.forName( args[0] );
Method m = c.getMethod( args[1], new Class [] {"I"} );
Object ret = m.invoke( null, null );
System.out.println(
"Invoked static method: " + args[1]
+ " of class: " + args[0]
+ " with no args/results: " + ret );
} catch ( ClassNotFoundException e ) {
// Class.forName() can’t find the class
} catch ( NoSuchMethodException e2 ) {
// that method doesn’t exist
} catch ( IllegalAccessException e3 ) {
// we don’t have permission to invoke that method
} catch ( InvocationTargetException e4 ) {
// an exception occurred while invoking that method
System.out.println(
"Method threw an: " + e4.getTargetException() );
}
}
}
```

Java 是一種功能強大的語言，用於網頁、機上盒、電視甚至汽車。

![](img/f80199d101da92d953f18eaa6205b48e_88_0.png)

```
40 LET PY=15
50 FOR W=1 TO 10
70 CLS
80 LET BY=INT (RND*28)
90 LET BX=0
100 FOR d=1 TO 20
110 PRINT AT PX,PY;"U"
120 PRINT AT BX,BY;"O"
130 IF INKEY$="P" THEN LET PY=P
140 IF INKEY$="O" THEN LET PY=P
135 FOR n=1 TO 100: NEXT n
140 IF PY>2 THEN LET PY=2
150 IF PY<2 THEN LET PY=27
160 LET SX=SX+1
185 PRINT AT BX-1,BY;""
190 NEXT d
200 IF PY=1 THEN LET S=S+1
210 PRINT AT 10,10;"SCORE=";S
500 FOR V=1 TO 1000: NEXT V
560 NEXT W
@ OK, Q:1
```

BASIC 曾經是早期 8 位家用電腦用戶學習的入門語言。

```
print(HANGMAN)
attempts = len(HANGMAN) - 1

while (attempts != 0 and "_" in word_guessed):
    print("You have {} attempts left".format(attempts))
    joined_word = " ".join(word_guessed)
    print("Current word: " + joined_word)

try:
    player_guess = str(input("Please select a letter between A-Z: ")).lower()
    except: print("That is not valid input. Please try again.")
    continue

if not player_guess.isalpha(): # check the input is a letter. Also checks a
    print("That is not a letter. Please try again.")
    continue

elif len(player_guess) > 1: # check the input is only one letter
    print("That is more than one letter. Please try again.")
    continue

elif player_guess in guessed_letters: # check if letter hasn’t been guessed
    print("You have already guessed that letter. Please try again.")
    continue

guessed_letters.append(player_guess)

for letter in range(len(chosen_word)):
    if player_guess == chosen_word[letter]:
        word_guessed[letter] = player_guess # replace all letters in the chosen

if player_guess not in chosen_word:
```

Python 是對 BASIC 的更現代詮釋，易於學習，是理想的初學者程式語言。

## 如何在 Linux 上设置 Python

虽然树莓派的操作系统包含最新、稳定的 Python 版本，但其他 Linux 发行版并不预装 Python 3。如果你不走树莓派路线，那么这里是如何检查和安装 Linux 的 Python。

## PYTHON PENGUIN

Linux 是一种如此多功能的系统，以至于很难确定做某件事的唯一方法。不同的发行版以不同的方式安装软件，因此本教程我们坚持使用 Linux Mint。

### STEP 1

首先你需要确定当前在 Linux 系统中安装了哪个版本的 Python。开始时，从发行版的菜单中进入终端会话，或按 `Ctrl+Alt+T` 键。

![](img/f80199d101da92d953f18eaa6205b48e_89_0.png)

### STEP 3

在我们的例子中我们同时安装了 Python 2 和 3；只要安装了 Python 3.x，那么我们的教程中的代码就会工作。最好检查一下发行版是否已更新到最新版本，因此输入：`sudo apt-get update && sudo apt-get upgrade` 来更新系统。

![](img/f80199d101da92d953f18eaa6205b48e_89_1.png)

### STEP 2

接下来在终端屏幕中输入 `python --version`。你应该在显示中看到与 Python 2.x 版本相关的输出。默认情况下，大多数 Linux 发行版都同时提供 Python 2 和 3，因为仍有大量代码可用于 Python 2。现在输入：`python3 --version`。

![](img/f80199d101da92d953f18eaa6205b48e_89_2.png)

### STEP 4

更新和升级完成后，再次输入：`python3 --version` 来查看 Python 3.x 是否已更新或甚至已安装；只要你有 Python 3.x，你就运行的是最新主要版本。3 之后的数字表示补丁和进一步的更新。它们通常是不必要的，但可能包含至关重要新元素。

![](img/f80199d101da92d953f18eaa6205b48e_89_3.png)

### STEP 5

然而，如果你想要最新、最前沿的版本，你需要从源代码构建 Python。开始时在终端中输入以下命令：

```
sudo apt-get install build-essential checkinstall
sudo apt-get install libreadline-gplv2-dev
libncursesw5-dev libssl-dev libsqlite3-dev tk-dev
libgdbm-dev libc6-dev libbz2-dev
```

![](img/f80199d101da92d953f18eaa6205b48e_90_0.png)

### STEP 6

打开你的 Linux 网络浏览器并前往 Python 下载页面：`www.python.org/downloads`。点击 Downloads 然后点击 Python Source 窗口下的按钮。这会打开一个下载对话框；选择一个位置并开始下载过程。

![](img/f80199d101da92d953f18eaa6205b48e_90_1.png)

### STEP 7
