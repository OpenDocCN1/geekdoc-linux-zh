+   c. test for hidden files

d. logical negation

+   6. The test command’s -o option is the _______________ operator.

	a. logical AND

	b. logical OR

	c. overwrite

	d. logical negation

+   7. The tr command __________________________.

	a. translates only what is typed at the keyboard

	b. translates on a line basis like sed

	c. translates on a character-by-character basis

	d. translates characters originating from within files only

+   8. The tr command to change phone records to contain all lowercase characters is

____________________.

	a. tr upper lower corp_phones

	b. tr [a-z] [A-Z] corp_phones

	c. cat corp_phones | tr [a-z] [A-Z]

	d. tr [A-Z] [a-z] < corp_phones

+   9. The test command returns a value of _______________ to indicate TRUE and

____________________ to indicate FALSE.

	a. 0, 1

	b. 1, 0

	c. blank err

	d. OK, !OK

+   10. The test command’s return value appears when you type _______________ at the

command line.

	a. echo $

	b. echo $?

	c. echo $-

	d. echo $.

# EXERCISES

+   1. Use the tr command to translate the phone records file to contain a hyphen as the field

separator instead of a colon (:). (Be sure to save the translated records to a different

file.)

+   2. Set an environment variable, RHL, to the value “Red Hat Linux,” and use the test and

echo $? commands to determine if it matches “Red Hat Linux” and “RED HAT

LINUX.” How can you tell which one matches?