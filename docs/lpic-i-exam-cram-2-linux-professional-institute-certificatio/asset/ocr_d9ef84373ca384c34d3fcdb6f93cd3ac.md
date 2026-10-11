9. Your boss wants all instances of an executive's name replaced with her title in a document. You've tried counting the instances and find you need to replace more than 500 of them. In the blank below, fill in just the name of the command that accomplishes this in a single command sequence:

![](bbox=[0.12, 0.205, 0.76, 0.23])

The correct answer is **sed**. There are no alternative correct answers.

10. You want to search a set of files for a given string but know only that the string begins with the characters **theo**, with a variety of endings. Which of the following, when used with **grep**, finds all the instances of text you want? (Choose all that apply.)

+   □ A. `\<theo`

+   □ B. `theo*`

+   □ C. `^theo`

+   □ D. `theo.*`

Answers A, B, and D are correct because these strings bring back a result for the text, with some notable differences in the output; however, they all work. Answer C is incorrect because the string `^theo` finds only the text at the beginning of a line in the files.