![](bbox=[0.29, 0.16, 0.0012, 0.47])

Figure 7-11 Redirecting and appending output

the append output symbol. The second command accomplishes the catenation described in the preceding caution box:

![](bbox=[0.34, 0.65, 0.64, 0.84])

The first command displays the contents of the orange file. The second command appends the contents of the pear file to the orange file. The final cat displays the result.

# Do not trust noclobber

Appending output is simpler than the two-step procedure described in the preceding caution box but you must be careful to include both greater-than signs. If you accidentally use only one and the noclobber feature is not set, the shell will overwrite the orange file. Even if you have the noclobber feature turned on, it is a good idea to keep backup copies of the files you are manipulating in case you make a mistake.

Although it protects you from overwriting a file using redirection, noclobber does not stop you from overwriting a file using cp or mv. These utilities include the -i (interactive) option that helps protect you from this type of mistake by verifying your intentions when you try to overwrite a file. For more information see the tip "cp can destroy a file" on page 164.

The next example shows how to create a file that contains the date and time (the output from date), followed by a list of who is logged in (the output from who). The first line in Figure 7-11 redirects the output from date to the file named whoson. Then cat displays the file. Next the example appends the output from who to the whoson file. Finally cat displays the file containing the output of both utilities.

# /dev/null: MAKING DATA DISAPPEAR

The /dev/null device is a data sink, commonly referred to as a bit bucket. You can redirect output that you do not want to keep or see to /dev/null and the output will disappear without a trace: