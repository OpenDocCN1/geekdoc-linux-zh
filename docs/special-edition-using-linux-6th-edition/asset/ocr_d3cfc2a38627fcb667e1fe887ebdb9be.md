# THE SPEC FILE

When you build packages, you use spec files to provide the information and scripts which automate the package-building process itself, and the information and scripts that are bundled as part of the package. This second set of scripts is used on the user’s system when the package is installed.

These two sets of information are intermingled in the spec file, without any distinction between them other than their names. However, it is important to remember which items are used on your system during the package build process, and which items are used on the end user’s system during package usage.

The spec file for a package is located in the SPECS directory and needs to have a filename consisting of the name of the package, the version number, and the extension .spec. For example, the name of the spec file for ed is ed-0.2.spec. For spec files that are used to produce multiple packages (such as -devel or -static packages), the base package name needs to be used for the filename.

A spec file includes two different kinds of entries: one-line fields and multiline sections. The one-line fields are placed at the top of the file in the header, and the sections follow. Most sections in the spec file contain Bourne shell scripts that run either during the package building process or on the end user’s system during package installation or removal. However, the %Description section is just a series of text lines that describe the package. Listing 17.1 shows the spec file for the ed package, which is used for the examples in this chapter. This spec file has been simplified to shorten it for inclusion in this book. If you have installed the ed source RPM, you can look at the unedited version at /usr/src/distribution/SPECS/ed-0.2.spec.

# LISTING 17.1 — THE SPEC FILE FOR ed (SIMPLIFIED)

```
Summary: GNU Line Editor
Name: ed
Version: 0.2
Release: 5
Group: Text processing/Editor
Copyright: GPL
Packager: rpw@lst.de (Roger Pook)
Icon: ed.gif
# URL: No WWW site found
Source0: ftp://prep.ai.mit.edu/pub/gnu/ed-0.2.tar.gz
# Patch: - optional -
# Provides: - optional -
# Requires: - optional -
# Conflicts: - optional -
BuildRoot: /tmp/ed-0.2
%Description
ed is a line-oriented text editor. It is used to create,
display, modify and otherwise manipulate text files. ed
is a restricted ed: it can only edit files in the current
directory and cannot execute shell commands.

%Prep
%setup
```