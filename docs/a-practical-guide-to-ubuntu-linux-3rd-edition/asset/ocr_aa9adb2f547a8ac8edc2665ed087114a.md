# EXERCISES

+   1. Explain the following unexpected result:
+   
+   ```bash
+   $ whereis date
+   date: /bin/date ...
+   $ echo $PATH
+   .:/usr/local/bin:/usr/bin:/bin
+   $ cat > date
+   echo "This is my own version of date."
+   $ ./date
+   Fri May 21 11:45:49 PDT 2010
+   ```

+   2. What are two ways you can execute a shell script when you do not have execute permission for the file containing the script? Can you execute a shell script if you do not have read permission for the file containing the script?

+   3. What is the purpose of the PATH variable?
+   
+   a. Set the PATH variable so that it causes the shell to search the following directories in order:
+   
+   • /usr/local/bin
+   
+   • /usr/bin
+   
+   • /bin
+   
+   • /usr/kerberos/bin
+   
+   • The bin directory in your home directory
+   
+   • The working directory