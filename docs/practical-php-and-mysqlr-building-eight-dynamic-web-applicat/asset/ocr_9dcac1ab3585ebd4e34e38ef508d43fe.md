subcategories, are displayed in the navigation bar. The `cat_relate` table specifies the relationships between different categories by connecting a parent `id` and child `id` to form the relationship. This will become clearer later in this chapter when you add categories.

# Implementing the Database

Start `phpMyAdmin`, create a new database called `news`, and add the following tables:

# The *categories* Table

+   - `id`. Make this a `SMALLINT` and turn on `auto_increment` in the `Extras` column. Set this field a primary key.
+   - `category`. Make this a `VARCHAR` and set the size to 20.
+   - `parent`. Make this a `TINYINT`.

# The *cat_relate* Table

+   - `id`. Make this a `SMALLINT` and turn on `auto_increment`. Set this field as a primary key.
+   - `parent_id`. Make this a `SMALLINT`.
+   - `child_id`. Make this a `SMALLINT`.

# The *users* Table

+   - `id`. Make this an `INT` and turn on `auto_increment`. Set this field as a primary key.
+   - `username`. Make this a `VARCHAR` and set the size to 10.
+   - `password`. Make this a `VARCHAR` and set the size to 32. In this project, `passwords` are encrypted to a 32-character-long value.
+   - `level1`. Make this a `TINYINT`.

# The *stories* Table

+   - `id`. Make this an `INT` (several questions are possible) and turn on `auto_increment`. Set this field as a primary key.
+   - `cat_id`. Make this a `SMALLINT`.
+   - `poster_id`. Make this a `SMALLINT`.
+   - `dateposted`. Make this a `DATETIME`.
+   - `subject`. Make this a `VARCHAR` with a length of 50.
+   - `body`. Make this a `TEXT`.