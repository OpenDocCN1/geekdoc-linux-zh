The file directory `documents` contains the files plan, dact, sys.A, new.hire, no.JSK, and AMG.reply. The directory `programs` contains the files wb, collect, and mon. At some point, you may decide to further categorize the files in a directory. This can be done by creating subdirectories and then placing each file into the appropriate subdirectory. For example, you might want to create subdirectories called memos, proposals, and letters inside your documents directory, as shown in Figure 1.2.

![](bbox=[0.133, 0.243, 0.687, 0.39])

*Figure 1.2*  Directories containing subdirectories

`documents` contains the subdirectories memos, proposals, and letters. Each of these subdirectories in turn contains two files: memos contains plan and dact; proposals contains sys.A and new.hire; and letters contains no.JSK and AMG.reply.

Although each file in a given directory must have a unique name, files contained in different directories do not. So you could have a file in your programs directory called dact, even though a file by that name also exists in the memos subdirectory.

# The Home Directory and Pathnames

The Unix system always associates each user of the system with a particular directory. When you log in to the system, you are placed automatically into your own directory (called your *home directory*).

Although the location of users’ home directories can vary from one system to the next, let’s assume that your home directory is called steve and that this directory is actually a subdirectory of a directory called users. Therefore, if you had the directories documents and programs, the overall directory structure would actually look something like Figure 1.3. A special directory named / (pronounced “slash”) is shown at the top of the directory tree. This directory is known as the root.

Whenever you are “inside” a particular directory (called your *current working directory*), the files contained within that directory are immediately accessible, without specifying any path information. If you want to access a file from another directory, you can either first issue a command to “change” to the appropriate directory and then access the particular file, or you can specify the particular file by its *pathname*.