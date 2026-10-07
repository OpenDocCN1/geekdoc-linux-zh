# The Concurrent Versions System [CVS] 149

CVS, like RCS, is easy to install from source. Download the tarfile from the CVS home page and unpack it in an appropriate directory by cd'ing to the directory and running the following commands

```
gzip -cd cvs-*.tar.gz | tar xvf -
```

That will create a directory cvs-X.XX (where X.XX is the version number). Next cd into that directory and run ./configure. If you are not root on the system, you might want to run ./configure --prefix=$HOME to build the software-install in your own home directory. Next run make followed by make. If you are not installing to your home directory and you are not root, you will have to su before the make step.

You will find prepackaged RPMs and Debian files to install CVS, but you can download source or binaries for Linux. To obtain a prepackaged version of CVS, you can install from your distribution CVS or download from multiple websites. For RPM packages, search for CVS at http://www.rpmfind.net/. For Debian packages, you can search for CVS at http://www.debian.org/dist/ You can then install the packages with your appropriate package manager.

# Basic CVS

CVS is more complicated than RCS but not difficult. All CVS commands follow this format:

```
cvs [cvs-option] command [cvs-command option] filename
```

This is probably different from commands you normally use, because it combines two commands in one. You start every CVS command with cvs and then any CVS options; next, the operation you'd like to perform, followed by any options that operation takes; and finally, the filename with which you're working. A real CVS command looks like this:

```
cvs commit filename
```

This command simply tells CVS to commit a file into the CVS repository and make it a new revision even if no changes occurred since the last one. In addition to full command-line names, such as commit, CVS offers abbreviated equivalents. For instance, cvs ci filename is the equivalent to cvs commit filename.