
## 13.4. The %prep Script

We could, if source-two.tgz creates the database subdirectory. If not, then it’ll be necessary to do it by hand. For the purposes of our example, let’s say that source-two.tgz wasn’t created to include the database subdirectory, so we’ll have to do it ourselves. Here’s our %prep script now:

```bash
%setup
%setup -T -D -a 1
mkdir database
cd database
gzip -dc /usr/src/redhat/SOURCES/source-two.tar.gz | tar -xvvf -
```

Here’s the resulting script:

```bash
cd /usr/src/redhat/BUILD
rm -rf cdplayer-1.0
gzip -dc /usr/src/redhat/SOURCES/source-zero.tar.gz | tar -xvvf -
if [ $? -ne 0 ]; then
	exit $?
fi
cd cdplayer-1.0
cd /usr/src/redhat/BUILD/cdplayer-1.0
chown -R root,root .
chmod -R a+rX,g+w,o-w .
cd /usr/src/redhat/BUILD
cd cdplayer-1.0
gzip -dc /usr/src/redhat/SOURCES/source-one.tar.gz | tar -xvvf -
if [ $? -ne 0 ]; then
	exit $?
fi
mkdir database
cd database
gzip -dc /usr/src/redhat/SOURCES/source-two.tar.gz | tar -xvvf -
```

The three commands we added to unpack the last set of sources were added to the end of the %prep script.

The bottom line to using the %setup macro is that you can probably get it to do what you want, but don’t be afraid to tinker. And even if %setup can’t be used, it’s easy enough to add the necessary commands to do the work manually. Above all, make sure you use the -t test option when testing your %setup macros, so you can see what commands they’re translating to.

### 13.4.2. The %patch Macro

The %patch macro, as its name implies, is used to apply patches to the unpacked sources.

In the following examples, our spec file has the following patch tag lines:

```text
Patch0: patch-zero
Patch1: patch-one
Patch2: patch-two
```

At its simplest, the %patch macro can be invoked without any options:

```text
%patch
```

Here are the resulting commands:

```bash
echo "Patch #0:"
patch -p0 -s < /usr/src/redhat/SOURCES/patch-zero
```

The `%patch` macro nicely displays a message showing that a patch is being applied, and then invokes the `patch` command to actually do the dirty work. There are two options to the `patch` command:

- The `-p` option, which directs `patch` to remove the specified number of slashes (and any intervening directories) from the front of any filenames specified in the patch file. In this case, nothing will be removed.
- The `-s` option, which directs `patch` to apply the patch without displaying any informational messages. Only errors from `patch` will be displayed.

How did the `%patch` macro know which patch to apply? Keep in mind that, like the source tag lines, every patch tag is numbered, starting at `0`. The `%patch` macro, by default, applies the patch file named on the `Patch` (or `Patch0`) tag line.

#### 13.4.2.1. Specifying Which patch Tag to Use

The `%patch` macro actually has two different ways to specify the `patch` tag line it is to use. The first method is to simply append the number of the desired `patch` tag to the end of the `%patch` macro itself. For example, in order to apply the patch specified on the `Patch2` tag line, the following `%patch` macro could be used:

```text
%patch2
```

The other approach is to use the `-P` option. This option is followed by the number of the `patch` tag line desired. Therefore, this line is identical in function to the previous one:

```text
%patch -P 2
```

Note that the `-P` option will not apply the file specified on the `Patch0` line, by default. Therefore, if you choose to use the `-P` option to specify `patch` numbers, you'll need to use the following format when applying patch `0`:

```text
%patch -P 0
```

#### 13.4.2.2. -p <#>: Strip <> Leading Slashes and Directories from patch Filenames

The `-p` (note the lowercase `p`) option is sent directly to the `patch` command. It is followed by a number, which specifies the number of leading slashes (and the directories in between) to strip from any filenames present in the patch file. For more information on this option, consult the `patch` man page.

#### 13.4.2.3. -b <name>: Set the Backup File Extension to <name>

When the patch command is used to apply a patch, unmodified copies of the files patched are renamed to end with the extension .orig. The -b option is used to change the extension used by patch. This is normally done when multiple patches are to be applied to a given file. By doing this, copies of the file as it existed prior to each patch are readily available.

#### 13.4.2.4. -E: Remove Empty Output Files

The -E option is passed directly to the patch program. When patch is run with the -E option, any output files that are empty after the patches have been applied are removed.

Now let's take %patch on a test drive.

#### 13.4.2.5. An Example of the %patch Macro in Action

Using the sample patch tag lines we've used throughout this section, let's put together an example and look at the resulting commands. In our example, the first patch to be applied needs to have the root directory stripped. Its %patch macro will look like this:

```text
%patch -p1
```

The next patch is to be applied to files in the software's lib subdirectory, so we'll need to add a cd command to get us there. We'll also need to strip an additional directory:

```text
cd lib
%patch -P 1 -p2
```

Finally, the last patch is to be applied from the software's top-level directory, so we need to cd back up a level. In addition, this patch modifies some files that were also patched the first time, so we'll need to change the backup file extension:

```text
cd ..
%patch -P 2 -p1 -b .last-patch
```

Here's what the %prep script (minus any %setup macros) looks like:

```text
%patch -p1
cd lib
%patch -P 1 -p2
cd ..
%patch -P 2 -p1 -b .last-patch
```

And here's what the macros expand to:

```bash
echo "Patch #0:"
patch -p1 -s < /usr/src/redhat/SOURCES/patch-zero
cd lib
echo "Patch #1:"
patch -p2 -s < /usr/src/redhat/SOURCES/patch-one
cd ..
echo "Patch #2:"
patch -p1 -b .last-patch -s < /usr/src/redhat/SOURCES/patch-two
```

No surprises here. Note that the %setup macro leaves the current working directory set to the software’s top-level directory, so our cd commands with their relative paths will do the right thing. Of course, we have environment variables available that could be used here, too.

#### 13.4.2.6. Compressed Patch Files

If a patch file is compressed with gzip, RPM will automatically decompress it before applying the patch. Here’s a compressed patch file as specified in the spec file:

`Patch: bother-3.5-hack.patch.gz`

This is part of the script RPM will execute when the %prep section is executed:

```bash
echo Executing: %prep
...
echo "Patch #0:"
gzip -dc /usr/src/redhat/SOURCES/bother-3.5-hack.patch.gz | patch -p1 -s
...
```

First, the patch file is decompressed using gzip. The output from gzip is then piped into patch. That’s about it for RPM’s macros. Next, let’s take a look at the %files list.

### 13.5. The %files List

The %files list indicates to RPM which files on the build system are to be packaged. The list consists of one file per line. The file may have one or more directives preceding it. These directives give RPM additional information about the file.

Normally, each file includes its full path. The path performs two functions. First, it specifies the file’s location on the build system. Second, it denotes where the file should be placed when the package is to be installed. (This is not entirely the case when a relocatable package is being built. For more information on relocatable packages, see Chapter 15.)

For packages that create directories containing hundreds of files, it can be quite cumbersome creating a list that contains every file. To make this situation a bit easier, if the %files list contains a path to a directory, RPM will automatically package every file in that directory, as well as every file in each subdirectory. Shell-style globbing, or wildcard expansion, can also be used in the %files list.

### 13.6. Directives for the %files List

The %files list may contain a number of different directives. They are used to do the following:

- Identify documentation and configuration files
- Ensure that a file has the correct permissions and ownership set
