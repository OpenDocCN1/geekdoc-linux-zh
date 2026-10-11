![](bbox=[0.0, 0.0, 1.0, 0.6])

# Reduce PDF file sizes with Minuimus

Shrink Ray

The Minuimus Perl script helps you save disk space by reducing the file size of PDF files with just a few commands.

*By Daniel Tibi*

Whether in an electronic library or an electronic file folder, PDF documents are ubiquitous. These digital documents can quickly eat up your disk space or fill up your cloud storage. Minuimus [1], a Perl script, helps you reduce PDF file sizes to free up space while preserving file quality.

# Installation

You can download the current version, Minuimus v3.7.1, from the project

page [2]. First unpack the ZIP file and then run the following commands one after the other:

```
sudo make deps
sudo make all
sudo make install
```

The first call checks the dependencies and installs any missing programs. The second command creates the required Minuimus files, and the third command copies them to the /usr/ bin/ directory. Upon completion, Minuimus will be available for all system users.

If you don't get the results you want with Minuimus's default settings, you can try one of the Minuimus options for potentially better results. Enter

```
minuimus.pl -h- help
```

to see a list of all the available options.

# Operating Principle

The principle behind Minuimus is simple: Minuimus first decompresses a PDF file and then recompresses it more efficiently. Minuimus draws on its own capabilities as well as a

![](bbox=[0.92, 0.78, 0.93, 0.94])