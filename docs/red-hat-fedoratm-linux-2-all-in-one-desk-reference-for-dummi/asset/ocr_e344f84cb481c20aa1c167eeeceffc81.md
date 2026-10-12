To add a PostgreSQL user, follow these steps:

+   1. **Log in as root.** Then type the following command in a terminal window:
+   
+      ```
+      su - postgres
+      ```
+   
+      You log in as *postgres*—the username under which the PostgreSQL database server runs. You have to perform PostgreSQL administrative tasks under this username.

+   2. **Type the following command in a terminal window:**
+   
+      ```
+      createuser
+      ```
+   
+      This utility program enables you to add PostgreSQL users. The program prompts for a username to add:

+   3. **Type the Linux username of the user to whom you are giving database privileges.**
+   
+      For example, to add myself as a user, I type my Linux username *naba*.

+   4. **Answer the next two prompts:**
+   
+      ```
+      Shall the new user be allowed to create databases? (y/n)
+      Shall the new user be allowed to create more new users? (y/n)
+      ```
+   
+      Typically, you don’t want a user to create databases or add new users, so you press N to these prompts.
+   
+      You can use this procedure to run `createuser` and add as many database users as you need.

# *Reviewing the steps to build the database*

Follow this basic sequence of steps to build a database:

+   1. **Design the database.**
+   
+      This step involves defining the tables and attributes that will be used to store the information.

+   2. **Create an empty database.**
+   
+      Before you can add tables, database systems require you to build an empty database.