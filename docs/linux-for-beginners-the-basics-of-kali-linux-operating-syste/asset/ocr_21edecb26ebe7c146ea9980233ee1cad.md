In any modern operating system, the file structure is hierarchical and depends on the directories. In general, the file system structure resembles a tree structure, each node being composed of a directory or folder, which contains other directories or files. In Windows, each disk drive is identified as a basic folder that serves as root to others. On Linux, there is a single root called / from which all files and directories hang, and that is independent of which devices are connected to the computer.

The path or path of a file or directory is the sequence of directories that must be traversed to access a certain file separated by /.

There are two forms of the path:

+   ❖ The absolute path that shows the entire path to a file, /home/luis/Carta.txt

+   ❖ The path relative to a certain directory, for example, if we cannot find the / home directory, the path relative to the file Letter.txt is Luis / Letter.txt

+   ○ To complicate matters further, all directories contain two special directories:

+   ❖ The current directory, represented by the point “.”

+   ❖ The parent directory represented by a colon “..”

Being in the directory/home you can access Carta.txt with /home/luis/Carta.txt (absolute path) or /luis/Carta.txt (relative path). In Luis as ./Carta.txt or simply Letter.txt.

The Linux file system follows all UNIX conventions, which means it has a structure determined, compatible and homogeneous with the rest of UNIX systems. Unlike in Windows or MS-DOS the file system on any Unix system is not directly linked to the hardware structure, that is, it does not depend on whether a given computer has 1, 2 or 7 hard drives to create the c:\, d:\ or m:\ drives.