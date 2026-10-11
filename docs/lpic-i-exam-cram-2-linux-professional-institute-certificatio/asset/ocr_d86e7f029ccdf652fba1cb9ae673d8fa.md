Functions are usually defined in the .bashrc file for a given user or in the /etc/bashrc file for all users. The syntax is exactly the same as on the command line, and functions are typically defined after any aliases because aliases are capable of being included in functions.

> **ALERT** Expect some questions about functions on the exam, including what a function is; how to create, modify, and remove them; how to view them; and what the correct syntax of a function is comprised of.

# # Understanding Shell Levels

One of the mysteries I want to clear up in this section is what happens to variables that are declared and exported when the shell exits.

For example, take the situation where you have an environment variable named **CHEESE** with a value of *wensleydale* and then you run a script where the same value is exported with a different value. It's important to know what happens to the value of the original, and also to the value of the latest exported version of the variable.

Here's how it works, step by step:

+   1. Open a shell session.

+   2. Declare and export the variable **CHEESE** with the following command:
+   
+      ```
+      export CHEESE=wensleydale
+      ```

+   3. Echo the value of **CHEESE** with the command shown here:
+   
+      ```
+      echo $CHEESE
+      ```
+   
+      This returns the following output:
+   
+      ```
+      wensleydale
+      ```

+   4. With the assurance that your variable contains the right value, create and save the following script in vi or your favorite editor:
+   
+      ```bash
+      #!/bin/bash
+      # filename = scriptfile
+      echo $CHEESE is set to $CHEESE
+      export CHEESE=gouda
+      TYPE=$CHEESE
+      echo "$TYPE is very good"
+      echo $CHEESE is set to $CHEESE
+      ```

+   5. Now set the file to be executable:
+   
+      ```
+      chmod +x scriptfile
+      ```