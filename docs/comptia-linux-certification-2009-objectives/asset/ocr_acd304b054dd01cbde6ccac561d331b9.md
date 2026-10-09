+   3. Edit the New_Policies.txt file for casing errors and generate the word count.

+   a. Enter `cat New_Policies.txt` to view the contents of the file.
b. Observe that casing of the letter “Y” in the word “EmploYees” is incorrect.
c. Enter `tr 'Y' 'y' < New_Policies.txt` to change the casing of the letter “Y” in the word “EmploYees.”
d. Observe that the casing of “Y” has changed.
e. Enter `wc -w New_Policies.txt` to count the words in the file.
f. Observe that the word count of the file is displayed.

+   4. Create a hard link for the file.

+   a. Enter `ln New_Policies.txt New_Policies_09.txt` to create a hard link for the file.
b. Enter `ls Nsw*` to view whether the hard link has been created.
c. Observe that the hard link is created.
d. Clear the terminal screen.