# Checking Spelling in pico

Another handy thing you can do in pico is chek yoor speling, as shown in Figures 4.7 and 4.8.

# To spell-check in pico:

+   1. pico hairyspiders
+   At the shell prompt, type pico and the filename of the file to edit.

+   2. Ctrl T
+   Pressing this command starts spell-checking the file. pico will stop at each misspelled word (Figure 4.7).

+   3. correctspelling
+   Type in the correct spelling for any words flagged as misspelled, or press Enter to accept the current spelling and move along to the next word.

# ✓ Tips

+   You can press Ctrl C to cancel spell-checking at any time.

+   Because the spell-checker in pico isn't full-featured, consider using an alternate spell-check program by specifying it on the command line, like pico -s ispell hairyspiders, so you can get a little more assistance. See Chapter 15 for more information.

+   When the entire document has been spell-checked, pico will tell you that it's done checking spelling, and you can continue editing the file (Figure 4.8).

![](bbox=[0.08, 0.12, 0.48, 0.38])

Figure 4.7 pico prompts you to correct the spelling of misspelled words.

![](bbox=[0.08, 0.48, 0.48, 0.68])

Figure 4.8 pico informs you when the procedure is complete.