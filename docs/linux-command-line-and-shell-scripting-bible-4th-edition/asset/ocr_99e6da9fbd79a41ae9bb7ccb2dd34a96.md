Because of potential typographical errors, the user account name entered needs verification. Doing so is easy because the code is already in place to handle asking questions:

```
line1="Is $user_account the user account "
line2="you wish to delete from the system? [y/n]"
get_answer
```

After the question is asked, the script must process the answer. The variable answer again carries the script user's answer to the question. If the user answers “yes,” the correct user account to delete has been entered and the script can continue. A case statement (see [Chapter 12]) is used to process the answer, and it is coded in a way to check for the multiple ways the answer “yes” can be entered.

```
case $answer in
y|Y|YES|yes|Yes|yEs|yeS|YeS|yES )
#
;;
*)
echo
	echo "Because the account, $user_account, is not "
	echo "the one you wish to delete, we are leaving the
script..."
	echo
	exit
;;
esac
```

That's tedious! Since we plan on only continuing the processing if the user answers a variation of “yes” to our question, we can simplify the case statement by stripping down the answer variable. To accomplish this task, we employ command substitution ([Chapter 11]), a pipe, and the cut command, which will allow us to reduce the characters in the answer variable. Specifically, the cut command's -c1 option strips everything from answer but the first character:

```
answer=$(echo $answer | cut -c1)
```

Now that we have to deal with only the first character, our case statement is more compact:

```
case $answer in
y|Y)
```