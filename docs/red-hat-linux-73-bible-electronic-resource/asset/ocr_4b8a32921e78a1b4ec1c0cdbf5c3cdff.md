# **RPM Versus Building from Source**

Binaries created in RPM format are easily installed, managed, and uninstalled using Red Hat tools. This is the recommended installation method for Red Hat Linux novices. Sometimes, however, building an application from source code may be preferable. Here are some arguments on both sides:

+   *   **RPM** — Installing applications from an RPM archive is easy. After the application is installed, there are both shell commands and GUIs for managing, verifying, updating, and removing the RPM application. You don't need to know anything about Makefiles or compilers. When you install an RPM package, RPM tools even check to make sure that other packages that the package depends on are installed. Because Red Hat has released RPM under the GNU, other Linux distributions have begun using it to distribute their software. Thus, most Linux applications are, or will be, available in RPM format.

+   *   **Source code** — It sometimes takes a while for a source-code package to be made into RPM binaries. If you use RPM you may find yourself with software that is several versions old, when you could simply download the latest source code and run a few tar and make commands. Also, by modifying the source code, you may be able to tailor the application to better suit your needs. When you compile the source code on your computer, it is also more likely to be optimized to run efficiently on your computer.

Here is a breakdown of the parts of a package name:

+   *   name — This is generally an all-lowercase string of characters that identifies the application.

+   *   dash (-)

+   *   version — This is shown as major to minor version number from left to right.

+   *   dot (.)

+   *   src or bin — This is optional, with src usually implied if no indication is given.

+   *   dot (.)

+   *   type of binary — This is optional and can include several different tags to describe the content of the binary archive. For example, i386 indicates binaries intended for Intel architectures (386, 486, Pentium, and so on) and SPARC indicates binaries for a Sparc CPU.

+   *   dot (.)

+   *   archive type — Often tar is used (.tar)

+   *   compression type — Often gzip is used (gzip)