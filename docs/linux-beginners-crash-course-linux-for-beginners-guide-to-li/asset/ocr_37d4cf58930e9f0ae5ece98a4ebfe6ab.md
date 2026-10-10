# ## Deleting content

You now know a few ways to move around in vi. Deleting works in a similar way; there are a number of different delete commands that you can use to define what you want to delete. The list below shows some of the ways to delete. Practice with them, but only after you have read the section on how to undo a deletion:

+   - x – delete a single character
+   - nx – delete n characters (e.g., 5x deletes five characters)
+   - dd – delete the current line
+   - dn – d followed by a movement command. Delete to where the movement command would have taken you (e.g., d5w means delete 5 words).

# ### Undoing

It is a fairly easy process to undo a delete in vi; just use the letter “u”.

+   - u – Undo the last action (you can keep pressing u to keep undoing)
+   - U (Note: capital) – Undo all changes to the current line