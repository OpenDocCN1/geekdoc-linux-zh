+   - A class is a Perl module that provides the methods to work with the object.
+   - A method is a Perl subroutine that expects the object reference as the first argument.

Object implementers have to follow certain rules and provide certain methods in a module that represents a class. However, you really don't need to know much about an object's implementation to use it in your Perl program. For practical purposes, all you need to know are the steps you have to follow when you use an object.

# Creating and accessing Perl objects

An especially useful Perl object is the Shell object, which is implemented by the Perl module Shell.pm. That module comes with the Perl distribution and is in the /usr/lib/perl5/5.8.1 directory (for Perl version 5.8.1).

As the name implies, the Shell object is meant for running shell commands from within Perl scripts. You can create a Shell object and have it execute commands.

To use the Shell object, follow these general steps:

+   1. Place the following line to include the Shell module in your program:
+   
+   ```
+   use Shell;
+   ```
+   
+   You must include this line before you create a Shell object.
+   
+   2. To create a Shell object, use the following syntax:
+   
+   ```
+   my $sh = Shell->new;
+   ```
+   
+   where $sh is the reference to the Shell object.
+   
+   3. Run Linux commands by using the Shell object and capture any outputs by saving to an appropriate variable. For example, to save the directory listing of the /usr/lib/perl5/5.8.0 directory in an array named @modules, write the following:
+   
+   ```
+   @modules = $sh->ls("/usr/lib/perl5/5.8.0/*.pm");
+   ```
+   
+   Then you can work with this array of Perl module filenames (that's what *.pm files are) any way you want. For example, to simply go through the array and print each string out, use the following while loop:
+   
+   ```
+   while(@modules)
+   {
+     $mod = shift @modules;
+     # Do whatever you want with the module name
+     print $mod;
+   }
+   ```