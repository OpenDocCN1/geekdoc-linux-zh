parameter. For example, this returns all the lines of the file **myfile.txt** that do not contain the word **hello**:
`$ grep -v "hello" myfile.txt`

You can also use regular expressions for your search term. For example, you can search **myfile.txt** for all references to cat, sat, or mat with this command:
`$ grep "[csm]at" myfile.txt`

Adding the **-i** parameter to that removes case sensitivity, matching Cat, CAT, MaT, and so on:
`$ grep -i [cms]at myfile.txt`

The output can also be controlled to some extent with the **-n** and **--color** parameters. The first tells **grep** to print the line number for each match, which is where it appears in the source file. The **--color** parameter tells **grep** to color the search terms in the output, which helps them stand out when among all the other text on the line. You choose which color you want, using the GREP_COLOR environment variable: `export GREP_COLOR=36` gives you cyan, and `export GREP_COLOR=32` gives you lime green.

This next example uses these two parameters to number and color all matches to the previous command:
`$ grep -in --color [csm]at myfile.txt`

Later you will see how important **grep** is for piping with other commands.

# Paging Through Output with less

The **less** command enables you to view large amounts of text in a more convenient way than the **cat** command. For example, your `/etc/passwd` file is probably more than a screen long, so if you run `cat /etc/passwd` you are not able to see what the lines at the top were. Using **less** `/etc/passwd` enables you to use the cursor keys to scroll up and down the output freely. Type **q** to quit and return to the shell.

On the surface, **less** sounds like a very easy command; however, it has the infamy of being one of the few Linux commands that have a parameter for every letter of the alphabet. That is, **-a** does something, **-b** does something else, **-c**, **-d**, **-e** … **-x**, **-y**, **-z** – they all do things, with some letters even differentiating between upper- and lowercase. Furthermore, these are only the parameters used to invoke **less**. After you begin viewing your text, even more commands are available to you. Make no mistake – **less** is a complex beast to master.

Input to **less** can be divided into two categories: what you type before running **less** and what you type while running it. The former category is easy, so we start there.