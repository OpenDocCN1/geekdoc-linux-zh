# **Match...**

The action described in the left column with the appropriate command in the right column.

+   ____ 1. find text forward					A. ?
+   ____ 2. put to the left or above			B. p
+   ____ 3. copy a big word back				C. y2{
+   ____ 4. find again in same direction		D. yy
+   ____ 5. find text back				E. /
+   ____ 6. copy two sentences back			F. yB
+   ____ 7. put to the right or below			G. P
+   ____ 8. find again in opposite direction	H. y$
+   ____ 9. copy entire line				I. n
+   ____ 10. copy to end of line				J. N

# **Commands to Remember**

/							find text forward
?							find text back
n							repeat the find in the same direction
N							repeat the find in the opposite direction
P							put the contents of the unnamed buffer to the right or below
P							put the contents of the unnamed buffer to the left or above
y [number] object		yank [optionally, some number of] *object* [s] into the unnamed buffer

# **Find, Copy, and Move with vi Summary**

+   * To copy text, you *yank* it.
+   * To insert text that you have yanked (to “paste,” in Windows and Macintosh terminology), you *put* the text.
+   * A *buffer* is a temporary storage area in the computer's memory.
+   * vi uses *unnamed buffers* to store text that you yank or delete.