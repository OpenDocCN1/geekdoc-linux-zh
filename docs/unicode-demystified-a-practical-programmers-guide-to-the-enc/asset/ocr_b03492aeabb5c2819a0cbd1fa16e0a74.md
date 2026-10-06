The first example uses aspell with the check action and no options. The appear-ance of the screen for the first misspelled word, teh, is shown. At the bottom of the screen is the menu of commands that can be given at this point. The nine numbered words all differ slightly from the misspelled word:

$ aspell check memo.txt
Here's a document for teh aspell utilitey
to check. It obviously needs proofing
quiet badly.

+   1) the 6) th
2) Te 7) tea
3) tech 8) tee
4) Th 9) Ted
5) eh 0) tel
i) Ignore I Ignore all
r) Replace R) Replace all
a) Add x) Exit

?
The next example uses the list action to display a list of misspelled words. The word quiet is not in the list—it is not properly used but is properly spelled:

$ aspell list < memo.txt
teh
aspell
utilitey
obviously

The last example also uses the uses list action. It shows a quick way to check the spelling of a word or two with a single command. The user gives the aspell list command then enters seperate temperature into aspell's input (the keyboard). After the user enters RETURN and CONTROL-D (to mark the end of file), aspell writes the misspelled word to standard output (the screen):

$ aspell list
seperate temperatureRETURN
CONTROL-D
seperate