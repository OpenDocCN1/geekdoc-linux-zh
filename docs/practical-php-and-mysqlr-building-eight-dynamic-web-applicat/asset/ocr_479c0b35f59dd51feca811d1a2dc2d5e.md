# The *mod_subvner* Table

+   ■ *id.* Make this an INT (several requests are possible) and turn on `auto_increment`. Set this field as a primary key.
+   ■ *sub_id.* Make this an INT.
+   ■ *user_id.* Make this an INT.
+   ■ *reasons* . Make this a TEXT.

# The *questions* Table

+   ■ *id.* Make this an INT (several questions are possible) and turn on `auto_increment`. Set this field as a primary key.
+   ■ *topic_id.* Make this an INT.
+   ■ *question.* Make this a VARCHAR with a length of 50.
+   ■ *answer.* Make this a TEXT.
+   ■ *addedby_id.* Make this an INT.
+   ■ *dateadded.* Make this a DATETIME.
+   ■ *active.* Make this a TINYINT.
+   ■ For this table, select the InnoDB table type.

# The *subjects* Table

+   ■ *id.* Make this an INT (several subjects are possible) and turn on `auto_increment`. Set this field as a primary key.
+   ■ *subject.* Make this a VARCHAR with a length of 20.
+   ■ *blurb.* Make this a TEXT.
+   ■ *owner_id.* Make this an INT.
+   ■ For this table, select the InnoDB table type.

# The *topics* Table

+   ■ *id.* Make this an INT (several topics are possible) and turn on `auto_increment`. Set this field as a primary key.
+   ■ *subject_id.* Make this an INT.
+   ■ *name.* Make this a VARCHAR with a length of 20.
+   ■ For this table, select the InnoDB table type.