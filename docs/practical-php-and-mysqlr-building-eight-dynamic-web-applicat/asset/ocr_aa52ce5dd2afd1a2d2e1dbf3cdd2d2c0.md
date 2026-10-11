![](bbox=[0.08, 0.11, 0.15, 0.17])

# NOTE

# Always Know Your Status

In the *orders* table is a field called *status*. The purpose of this field is to indicate at what point in the shopping cart the user has progressed. This field has four possible values:

+   0 The user is still adding items to her shopping cart.
+   1 The user has entered her address.
+   2 The user has paid for the item.
+   10 The administrator has confirmed the transaction and sent the item.

# The *admins* Table

+   id. Make this a TINYINT (lots of users are possible) and turn on auto_increment. Set this field as a primary key.
+   username. Make this a VARCHAR with a length of 10.
+   password. Make this a VARCHAR with a length of 10.

# The *categories* Table

+   id. Make this a TINYINT (there will be few categories) and turn on auto_increment in the Extras column. Make this field a primary key.
+   name. Make this a VARCHAR and set the size to 20. (It is unlikely a category title will be longer than 20 letters.)

# The *customers* Table

+   id. Make this an INT (lots of users are possible) and turn on auto_increment. Set this field as a primary key.
+   forename. Make this a VARCHAR with a length of 50.
+   surname. Make this a VARCHAR with a length of 50.
+   addl. Make this a VARCHAR with a length of 50.
+   add2. Make this a VARCHAR with a length of 50.
+   add3. Make this a VARCHAR with a length of 50.
+   postcode. Make this a VARCHAR with a length of 10.
+   phone. Make this a VARCHAR with a length of 20.
+   email. Make this a VARCHAR with a length of 100.
+   registered. Make this a TINYINT.