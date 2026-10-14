class file called `AnotherClass.class` that you want to add to your `jar` file, you’d use the format:

```
```shell
$ jar uf myjar.jar AnotherClass.class
```
```

After creating a jar file you can list the contents of the file using the format:

```
```text
$ mf myjar.jar
META-INF/
META-INF/MANIFEST.MF
MyTestClass.class
AnotherClass.class
$
```
```

Notice that by default the `jar` process adds a file called `MANIFEST.MF`. This file is called the manifest, and it is used to track the features of the classes contained in the `jar` file. We’ll experiment with that file in a little bit.

To extract the files contained in the `jar` file, you’d use the format:

```
```shell
$ jar xf myjar.jar
$ ls -al
total 20
drwxr-xr-x 3 rich rich 4096 2008-11-18 05:36 .
drwxr-xr-x 37 rich rich 4096 2008-11-18 06:23 ..
drwxr-xr-x 2 rich rich 4096 2008-11-18 06:18 META-INF
-rw-r--r-- 1 rich rich 928 2008-11-18 06:23 myjar.jar
-rw-r--r-- 1 rich rich 727 2008-11-18 06:33 MyTestClass.class
-rw-r--r-- 1 rich rich 727 2008-11-18 06:35 AnotherClass.class
$
```
```

The manifest file helps the JVM determine what files are in the `jar` file and the location of the class that contains the main method (called the application entry point). Take a look at the default manifest file that the `jar` process created:

```
```shell
$ cd META-INF
$ ls -al
total 12
drwxr-xr-x 2 rich rich 4096 2008-11-18 05:18 .
drwxr-xr-x 3 rich rich 4096 2008-11-18 06:36 ..
-rw-r--r-- 1 rich rich 70 2008-11-18 06:18 MANIFEST.MF
$ cat MANIFEST.MF
Manifest-Version: 1.0
Created-By: 1.6.0_0 (Sun Microsystems Inc.)
$
```
```

The default manifest shows generic information. You can use that file to give the JVM specific instructions about your application, such as the entry point of your Java application. To do that, you must create a manifest file to add to your jar file. The `jar` program will add the information from your manifest file to the standard manifest information.

To specify the class that contains the `main` method, create a manifest file called `Manifest.txt` and use the `Main-Class:` tag to define the class that contains the main class method. After adding the file, the contents of your `Manifest.txt` file should look like this:

```
```text
$ cat Manifest.txt
Main-Class: MyTestClass
$
```
```