# Chapter 23: Software Development on Ubuntu

FIGURE 23-12
Running the sample application in Eclipse

![](bbox=[0.039, 0.163, 0.7, 0.532])

In my opinion, the easiest way to import an existing project into Eclipse is as a tarball that contains the source. This enables you to import a pristine version of the source code and also provides a convenient way to keep track of exactly what was in when you moved it into Eclipse, by archiving the tarball.

Preparatory to beginning the import process, cd to the top level of your source project directory and clean the project to remove object code, backup files, and any other items that you don't want to import. You will want to generate a source tarball for your project from the top level of its source code directory so that the files comprise your project are imported into the top level of your Eclipse project rather than being created in a sub는데, which would happen if you imported a vanilla tarball that you retrieved from the Web or as a backup of your project. In my case, I prepare the tarball with commands like the following:

```
$ cd pop3check-0.100.03
$ make clean
$ tar czf ../pop3check.gz *
```

Tarball in hand, start Eclipse using the Applications Eclipse command, and create an Eclipse project that corresponds to the source project that you are importing by using File New Project selector. Since we are importing a complete project that contains a Makefile, you will need to create a project that understands how to use Makefiles. Select the C