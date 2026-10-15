+   - **$path**. The content of this variable is passed to the PATH environment variable.
+   - **$dspam**. Activate the dspam content filter (http://www.nuclearelephant.com/projects/dspam/).
+   - **$MAXLEVELS**. Maximum recursion level for extraction and decoding.
+   - **$MAXFILES**. Maximum number of extracted files.
+   - **$MIN_EXPANSION_QUOTA**, **$MAX_EXPANSION_QUOTA**. Minimum and maximum storage size (in bytes) that is available for mail extraction.
+   - **$sa_spam_subject_tag**. String that is prepended to the subject header when message exceeds **$sa_tag2_level_deflt** level.
+   - **@*_lovers_maps**. Email to the specified recipients is not examined and filtered.
+   - **@blacklist_sender_maps**. A message from a blacklisted envelope sender address is marked as spam.
+     A **@whitelist_sender_maps** is also available. Mail with sender addresses from this array are delivered although they are marked as spam.
+   - **@score_sender_maps**. Using this variable you can add or subtract a specified value to/from the spam value.

The next variables (beginning with **@viruses_that_fake_sender_maps**) contain regular expressions to filter mails.

Many regular expressions are predefined and you can enable them by removing the comment hash sign at the beginning of the line(s).

Of course you can modify the regular expressions if they do not fit your needs.