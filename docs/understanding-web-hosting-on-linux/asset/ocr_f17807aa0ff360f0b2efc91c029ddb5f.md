# Programming Assignment

# Exercise 1: Create Directory Reports

+   1. Create a report file that lists the contents of your home directory.
   a) Put a header in the report file that contains your full name and the name of your directory.
   b) Make sure the list contains the size of each file.
2. Using the Java jar utility, list the contents of the servlet.jar in /opt/tomcat/lib.
3. Using the find command:
   a) List all the HTML files under /opt/tomcat/webapps/examples.
   b) List all the JSP files under /opt/tomcat/webapps/examples.
4. Piping output:
   a) The file listing from step 2 is overly verbose. Often, you will have to look in .jar files to see if a particular Java class is in that. Pipe the output from step 2 to grep to search for the HttpServlet class.
   b) Pipe step 3's output through the xargs utility. (The xargs output, without qualifying a command, does not do much. It just takes input and, delimited by spaces or lines, iteratively invokes the command that follows.)
   c) To make use of xargs, run the find commands from step 3 piping the output through xargs, but this time qualify the grep command as an option to xargs. Ask grep to list the JSP files that contain a reference to the special request variable.

> Hint: Here's how you would list the HTML files that have a <FORM> tag:
$ find /opt/tomcat/webapps/examples -name "*.html" | xargs grep FORM

# Exercise 2: Environment Variables

+   1. List all environment variables.
2. Create a new environment variable using your last name. (Remember, use all uppercase for environment variables.) Set that environment's value to be your first name.
3. Append to the Java CLASSP environment variable a qualifier to Tomcat's servlet.jar file, using the following strategy:
   a) Change your current directory to /opt/tomcat/lib.
   b) Modify CLASSPATH using the "print working directory" command in back quotes:
   $ CLASSPATH=$CLASSPATH:`pwd`/servlet.jar
   The 'pwd' command should be interpreted as /opt/tomcat/lib and the CLASSPATH should be modified accordingly.
4. List all environment variables again. Pipe the output to the printer.