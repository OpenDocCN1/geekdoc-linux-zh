If this is a new file, you should see something similar to the following:

```
~
~
~
~"/tmp/test" [New File]
```

The box at the top represents where your cursor is. The bottom line keeps you informed about what is going on with your editing (as filer you just opened a new file). Between, there are tildes (~) because there is no text in the file yet. Now here's the intimidating part: There are no hints, menus, or icons to tell you what to do. On top of that, you can't just typing. If you do, the computer is likely to beep at you. And some people complain that Linux isn't friendly.

The first things you need to know are the different operating modes: command and input. The vi editor starts in command mode. Before you can add or change the text, you have to type a command (one or two letters and an optional number) to tell vi what you want to do. Case is important, so use and lowercase as shown in the examples! To get into input mode, type an input command. To start out, type either of the following:

+   - a The command. After it, you can input text that starts to the right of the cursor.
- i The insert command. After it, you can input text that starts to the left of the cursor.

Type a few words and press Enter. Repeat a few times until you have a few lines of text. When you're finished typing, press Esc to return to command mode. Now that you have a file with some text in it, try moving around your text with the following keys or letters:

> Remember the Esc key! It places you back into command mode.

+   - Arrow keys—Move the cursor up, down, left, or right in the file one character at a time. If you move left and right you can use Backspace and the space bar, respectively. If you prefer to keep your fingers on the keyboard, move the cursor with h (left), l (right), j (down), or k (up).
- w—Moves the cursor to the beginning of the next word.
- b—Moves the cursor to the beginning of the previous word.
- 0 (zero)—Moves the cursor to the beginning of the current line.
- S—Moves the cursor to the end of the current line.
- H—Moves the cursor to the upper-left corner of the screen (first line on the screen).