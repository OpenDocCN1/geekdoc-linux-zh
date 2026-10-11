# Compile the Source File

The Java compiler, Javac, compiles the source file and translates its text into instructions that the Java Virtual Machine (Java VM) can understand. The compiler then stores these instructions into a byte code file.

+   1. Now, bring up another shell window. Change your current directory to the directory where your file is located to compile your source file. For example, if your source directory is /home/Mahendra/java, you would type the following command at the prompt and press return
+      `cd /home/smith/java`

If you enter pwd at the prompt, you see the current directory, which in this example has been changed to /home/smith/java.

If you enter ls at the prompt, you see your file: sample.java.

+   1. Type the following command and then press Return to compile your file:
+      `javac sample.java`

After compiling if you see the following error message:

```
javac: Command not found
```

Then, it means Linux is not able to find the Java compiler, Javac.

+   1. You can locate the javac compiler in Linux by typing the path where you have installed the Java 2 Platform Suppose: you have installed the Java 2 Platform (J2SE) in /usr/java/jdk1.4. In this case, you can type the following command at the prompt and press Return:
+      `/usr/java/jdk1.4/javac sample.java`

The compiler now has generated a Java byte code file, sample.class.

+   1. At the prompt, type ls to verify the new file is there.

# Run the Program

The Java VM is implemented by a Java interpreter called java. This interpreter translates the byte codes into instructions that can be understood by your computer.

+   1. In the same directory, enter at the prompt:
+      `java sample`

When you run the program you need to enter two numbers when the black command line window appears. The program should then write out those two numbers plus the percentage computed by the program.

If you receive the following error message:

+   Exception in thread "main" java.lang.NoClassDefFoundError:sample
+   Then it means, Java cannot find your byte code file, sample.class.