+   12. Delete **tempfile1**.
+   a.  Type `rm tempfile1`
+   b.  Press <Enter>

Next you will delete **tempfile2**, **tempfile3**, and **tempfile5**. You could type the command line `rm tempfile2` three times, substituting the appropriate number each time. This would not be a lot of work, granted. But suppose now that there are ten files in your directory—or twenty. Suddenly, you're faced with some burdensome typing. You can use `rm -i *` to delete files selectively. The wildcard * means “everything.” So this command line says, in effect, “Delete everything, but let me confirm the deletion of each file individually.”

+   13. Delete **tempfile2**, **tempfile3**, and **tempfile5** selectively with `rm -i *`.
+   a.  Type `rm -i *`
+   b.  Press <Enter>

The system responds with something similar to `rm: remove 'tempfile2'?`

+   c.  Press the letter “y” to confirm.
+   d.  Press <Enter>

The system responds with something similar to `rm: remove 'tempfile3'?`

+   e.  Press the letter “y” to confirm.
+   f.  Press <Enter>

The system responds with something similar to `rm: remove 'tempfile4'?`

+   g.  Press the letter “n” to reject this deletion.
+   h.  Press <Enter>

The system responds with something similar to `rm: remove 'tempfile5'?`

+   i.  Press the letter “y” to confirm.
+   j.  Press <Enter>

The system responds with something similar to `rm: remove 'tempfile6'?`