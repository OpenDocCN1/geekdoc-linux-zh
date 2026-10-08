+   1. To leave vi temporarily to find the current date and time:
1. Type :date and press Enter.
You see today's date and instructions for returning to command mode.
2. Press Enter to return to command mode.

# Changing Your Display While Editing

Besides using the vi editing commands, you can also set options in vi to control editing parameters such as line number display and whether case matters in searches. Turn on line numbering when you want to work with a range of lines, for example, when you're deleting or cutting and pasting a block of text. Then you can refer to the line numbers to specify the text. You decide to delete the last three lines from your memo. Turn on line numbering first, and then use a delete command.

+   To use automatic line numbering:
1. Type :set number and press Enter.
Your redrawn screen shows line numbers to the left of the text. Your screen should look like the one in Figure 3-11.

![](bbox=[0.2, 0.52, 0.77, 0.85])

Line numbers are for reference only. They are not part of the file. Now you can use these reference numbers to delete the last three lines in the file.