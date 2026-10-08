# mkdir

# **mkdir - Make a directory.**

![](bbox=[0.85, 0.11, 0.96, 0.23])

mkdir(1)                                    mkdir(1)

NAME
mkdir - make a directory

SYNOPSIS
mkdir [-p] [-m mode] dirname ...

DESCRIPTION
mkdir creates specified directories in mode 0777 (possibly altered by umask unless specified otherwise by a -m mode option (see umask(1)). Standard entries.. (for the directory itself) and .. (for its parent) are created automatically. If dirname already exists, mkdir exits with a diagnostic message, and the directory is not changed.

+   Options
mkdir recognizes the following command-line options:
- **-m mode**: After creating the directory as specified, the file permissions are set to mode, which is a symbolic mode string as defined for chmod (see chmod(1)). The umask(1) has precedence over -m.
- **-p**: Intermediate directories are created as necessary. Otherwise, the full path prefix of dirname must already exist. mkdir requires write permission in the parent directory.

For each directory name in the pathname prefix of the dirname argument that is not the name of an existing directory, the specified directory is created using the current umask setting, except that the equivalent of chmod u+w is done on each component to ensure that mkdir can create lower directories regardless of the setting of umask. Each directory name in the pathname prefix of the dirname argument that matches an existing directory is ignored without error. If an intermediate path component exists, but has permissions set to prevent writing or searching, mkdir fails with an error message. If the dirname argument (including pathname prefix) names an existing directory, mkdir fails with an error message.

If the -m option is used, the directory specified by dirname (excluding directories in the pathname prefix) is created with the permissions specified by mode.