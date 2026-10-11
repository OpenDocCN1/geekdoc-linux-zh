If you don't specify a file, any input you enter is stored into the work buffer until you save it to a file. Because vi works entirely in memory, the program is very fast and doesn't suffer from traditional file-size limitations. The work buffer can read any file format written to disk. Within the size of the memory available to vi, the editor can read any line size. One newline or linefeed character delimits a line. The size of the file you can create in vi is limited only by available disk space.

> **WARNING** If you open a file that contains a variety of characters beyond simple alphanumeric and punctuation characters, you have either opened an application document or a binary executable file. In either case, you can easily do serious damage to that file if you remove any of those characters. You should close the file immediately by issuing the :q! command.

# ## vi Modes

The vi editor is modal, which means you can perform certain actions only when you are in a particular state of the editor. There are several main modes of operation in vi:

**Command mode** When you first open a file using the vi editor, you will already be in Command mode. In Command mode, you can create and open files, specify cursor positioning and editing commands, save your work to a file, and so forth. Keystrokes you enter in Command mode aren't shown on your screen but are acted upon immediately. You can return to the Command mode at any time by pressing the Esc key.

**Entry mode** In Entry mode, you can enter text into the display on your screen. To enter Entry mode, you must first type an input command, such as i (inserts text), o (overwrites text), or a (appends text) to enter a submode of the Entry mode. These different submodes allow you to add and edit text and differ primarily in the manner in which text is added and removed from your display.

**Last-Line mode** When in Command mode, you can type a colon (: ) to move to the end of the file on your display, which is called the Last-Line mode. In Last-Line mode, you enter into a single-line command processor in which you can issue commands before you press the Return (or Enter) key to enter the Input state of the Entry mode.

Figure 16.4 shows how you move between the main vi modes and some of the primary submodes. Mostly, you will be working in the Command mode specifying actions and in the various Entry submodes (such as Insert or Overwrite) entering and editing