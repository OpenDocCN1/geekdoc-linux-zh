# **EXERCISE 2.1 (continued)**

+   6.  Type **rpm -qpi zsh-4.3.4-4mdv2008.0.x86_64.rpm**. (You’ll need to add a complete path to the package file if it’s not in your current directory.) The system should respond by displaying information about the package, such as the version number, the vendor, the hostname of the machine on which it was built, and a package description.

+   7.  Type **rpm -ivh zsh-4.3.4-4mdv2008.0.x86_64.rpm**. The system should install the package and display a series of hash marks (#) as it does so.

+   8.  Type **rpm -q zsh**. The system should respond with the complete package name, including the version and build numbers. This response verifies that the package is installed.

+   9.  Type **zsh**. This launches a Z shell, which functions much like the more common bash and tcsh shells. You’re likely to see your command prompt change slightly, but you can issue most of the same commands you can use with bash or tcsh.

+   10. Type **rpm -V zsh**. The system shouldn’t produce any output—just a new command prompt. The verify (−V or --verify) command checks the package files against data stored in the database. Immediately after installation, most packages should show no deviations. (A handful of packages will be modified during installation, but zsh isn’t one of them.)

+   11. Type **rpm -e zsh**. The system shouldn’t produce any output—just a new command prompt. This command removes the package from the system. Note that you’re removing the zsh package while running the zsh program. Linux continues to run the zsh program you’re using, but you’ll be unable to launch new instances of the program. Some programs may misbehave if you do this because files will be missing after you remove the package.

+   12. Type **exit** to exit zsh and return to your normal shell.

+   13. Type **rpm -q zsh**. The system should respond with a **package zsh is not installed** error because you’ve just uninstalled the package.

+   14. Type **yum install zsh**. The system should check your repositories, download zsh, and install it. It will ask for confirmation before beginning the download.

+   15. Type **rpm -q zsh**. The results should be similar to those in step 8, although the version number may differ.

+   16. Type **rpm -e zsh**. This step removes zsh from the system but produces no output, just as in step 11.

The final three steps will work only if your distribution uses Yum.