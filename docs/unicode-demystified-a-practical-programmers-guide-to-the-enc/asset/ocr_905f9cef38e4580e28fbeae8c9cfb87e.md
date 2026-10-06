# Screen

The terminal screen is a window that opens onto part of the Work buffer. You can position this window so that it shows different portions of the Work buffer.

# Repeat Factor

A number that precedes a Unit of Measure (page 460) is a Repeat Factor. Just as the 5 in 5 inches causes you to consider 5 inches as a single Unit of Measure, a Repeat Factor causes vim to group more than one Unit of Measure and consider it as a single Unit of Measure. For example, the command w moves the cursor 1 word. The command 5w moves the cursor forward 5 words, and 250w moves it forward 250 words. If you do not specify a Repeat Factor, vim assumes that you mean one Unit of Measure. If the Repeat Factor would move the cursor past the end of the file, it is left at the end of the file.

# Chapter Summary

This summary of vim includes all the commands covered in this chapter, plus a few more.

# Starting vim

| vim filename | Edits filename starting at line1 |
| vim +n filename | Edits filename starting at line n |
| vim + filename | Edits filename starting at the last line |
| vim +/-pattern filename | Edits filename starting at the first line containing pattern |
| vim -r filename | Recovers filename after a system crash |
| vim -R filename | Edits filename readonly |

# Moving the Cursor by Units of Measure

You must be in Command mode to use commands that move the cursor by Units of Measure. They are the Units of Measure that you can use in Change, Delete, and Yank commands. Each of these commands can be preceded by a Repeat Factor.