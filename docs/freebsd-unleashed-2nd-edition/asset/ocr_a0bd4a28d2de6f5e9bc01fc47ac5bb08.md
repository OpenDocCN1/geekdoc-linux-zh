# File Operations and Exiting vi

Several vi commands are related to loading and saving files. Table 6.6 shows the various commands available for these actions.

**TABLE 6.6 File Operations in vi**
| Command | Action |
| :--- | :--- |
| :wq | Saves changes to the current file and then exits. |
| :w | Saves changes to the current file. |
| :w! | Saves changes to the current file, overwriting a file of the same name if it already exists. |
| :q | Quits vi. If there are unsaved changes, vi complains and does not quit. |
| :q! | Quits vi even if there are unsaved changes. All unsaved changes will be lost. |
| :e filename | Loads the specified file into vi for editing. If the specified file does not exist, a new file will be created. |
| :e! | Loses all changes and reloads the saved file from the disk. |
| :wq | Saves changes to the current file and then exits (the same as :wq). |

**CAUTION**

Note that the ! option on the end of several of the commands in Table 6.6 forces the action to take place. You will not be prompted before the action is taken if you have unsaved changes in your document. For example, :q! will exit vi immediately without asking first whether you want to save any changes. Use the ! option with care.

# Searching and Replacing Text in vi

Several commands are available for performing a search-and-replace operation in vi. Table 6.7 lists these commands and their actions.

**TABLE 6.7 Search and Replace Commands in vi**
| Command | Action |
| :--- | :--- |
| /pattern | Here, *pattern* is what to search for. vi searches forward in the file for the first occurrence of the specified pattern. |
| / | Repeats the last search, finding the next occurrence of the pattern in the file. |
| ?pattern | Here, *pattern* is what to search for. vi searches backward in the file for the first occurrence of the specified pattern. |
| ? | Repeats the last search, finding the previous occurrence of the pattern in the file. |
| % | Moves to the matching parenthesis or brace for the one that the cursor is currently on. This is useful to programmers. |
| :s/pattern1/pattern2 | Replaces each occurrence of *pattern1* with *pattern2* on the current line. |
| :%s/pattern1/pattern2 | Replaces every occurrence of *pattern1* with *pattern2* in the entire file. |