
## Booleans and General Values

Booleans and false can be spelled as no, off, false, or 0.

When converting values to the canonical form using *bool* type specifier, *git config* will ensure that the output is "true" or "false" (spelled in lowercase).

### Integer

The value for many variables that specify various sizes can be suffixed with k, M, ... to mean "scale the number by 1024", "by 1024x1024", etc.

### Color

The value for a variable that takes a color is a list of colors (at most two) and attributes (at most one), separated by spaces. The colors accepted are normal, black, red, green, yellow, blue, magenta, cyan and white; the attributes are bold, dim, ul, blink and reverse. The first color given is the foreground; the second is the background. The position of the attribute, if any, doesn't matter. Attributes may be turned off specifically by prefixing them with no (e.g., noreverse, noul, etc).

Colors (foreground and background) may also be given as numbers between 0 and 255; these use ANSI 256-color mode (but note that not all terminals may support this). If your terminal supports it, you may also specify 24-bit RGB values as hex, like #ff0ab3.

The attributes are meant to be reset at the beginning of each item in the colored output, so setting color.decorate.branch to black will paint that branch name in a plain black, even if the previous thing on the same output line (e.g. opening parenthesis before the list of branch names in log --decorate output) is set to be painted with bold or some other attribute.

## Variables

Note that this list is non-comprehensive and not necessarily complete. For command-specific variables, you will find a more detailed description in the appropriate manual page.

Other git-related tools may and do use their own variables. When inventing new variables for use in your own tool, make sure their names do not conflict with those that are used by Git itself and other popular tools, and describe them in your documentation.

### advice.*

These variables control various optional help messages designed to aid new users. All *advice.* variables default to *true*, and you can tell Git that you do not need help by setting these to *false*:

#### pushUpdateRejected

Set this variable to *false* if you want to disable *pushNonFFCurrent*, *pushNonFFMatching*, *pushAlreadyExists*, *pushFetchFirst*, and *pushNeedsForce* simultaneously.

#### pushNonFFCurrent

Advice shown when `git push` fails due to a non-fast-forward update to the current branch.

#### pushNonFFMatching

Advice shown when you ran `git push` and pushed matching refs explicitly (i.e. you used : or specified a refspec that isn’t your current branch) and it resulted in a non-fast-forward error.

#### pushAlreadyExists

Shown when `git push` rejects an update that does not qualify for fast-forwarding (e.g., a tag).

#### pushFetchFirst

Shown when `git push` rejects an update that tries to overwrite a remote ref that points at an object we do not have.

#### pushNeedsForce

Shown when `git push` rejects an update that tries to overwrite a remote ref that points at an object that is not a commit-ish, or make the remote ref point at an object that is not a commit-ish.

#### statusHints

Show directions on how to proceed from the current state in the output of `git status`, in the template shown when writing commit messages in `git commit`, and in the help message shown by `git switch` when switching branch.

#### statusUoption

Advise to consider using the -u option to `git status` when the command takes more than 2 seconds to enumerate untracked files.

#### commitBeforeMerge

Advice shown when `git merge` refuses to merge to avoid overwriting local changes.

#### resolveConflict

Advice shown by various commands when conflicts prevent the operation from being performed.

#### implicitIdentity

Advice on how to set your identity configuration when your information is guessed from the system username and domain name.

#### detachedHead

Advice shown when you used `git checkout` to move to the detach HEAD state, to instruct how to create a local branch after the fact.

#### amWorkDir

Advice that shows the location of the patch file when `git am` fails to apply it.

#### rmHints

In case of failure in the output of `git rm`, show directions on how to proceed from the current state.

### core.fileMode

Tells Git if the executable bit of files in the working tree is to be honored.

Some filesystems lose the executable bit when a file that is marked as executable is checked out, or checks out a non-executable file with executable bit on. `git init` or `git clone` probe the filesystem to see if it handles the executable bit correctly and this variable is automatically set as necessary.

A repository, however, may be on a filesystem that handles the filemode correctly, and this variable is set to *true* when created, but later may be made accessible from another environment that loses the filemode (e.g. exporting ext4 via CIFS mount, visiting a Cygwin created repository with Git for Windows or Eclipse). In such a case it may be necessary to set this variable to *false*. See `core.fileMode`.

The default is true (when core.fileMode is not specified in the config file).

### core.ignoreCase

If true, this option enables various workarounds to enable Git to work better on filesystems that are not case sensitive, like FAT. For example, if a directory listing finds “makefile” when Git expects “Makefile”, Git will assume it is really the same file, and continue to remember it as “Makefile”.

The default is false, except `git init` or `git clone` will probe and set core.ignoreCase true if appropriate when the repository is created.

### core.precomposeUnicode

This option is only used by Mac OS implementation of Git. When core.precomposeUnicode=true, Git reverts the unicode decomposition of filenames done by Mac OS. This is useful when sharing a repository between Mac OS and Linux or Windows. (Git for Windows 1.7.10 or higher is needed, or Git under cygwin 1.7). When false, file names are handled fully transparent by Git, which is backward compatible with older versions of Git.

### core.protectHFS

If set to true, do not allow checkout of paths that would be considered equivalent to .git on an HFS+ filesystem. Defaults to true on Mac OS, and false elsewhere.

### core.protectNTFS

If set to true, do not allow checkout of paths that would cause problems with the NTFS filesystem, e.g. conflict with 8.3 “short” names. Defaults to true on Windows, and false elsewhere.

### core.trustctime

If false, the ctime differences between the index and the working tree are ignored; useful when the inode change time is regularly modified by something outside Git (file system crawlers and some backup systems). See `core.checkStat`. True by default.

### core.checkStat

Determines which stat fields to match between the index and work tree. The user can set this to *default* or *minimal*. *Default* (or explicitly *default*), is to check all fields, including the sub-second part of mtime and ctime.

### core.quotePath

The commands that output paths (e.g. `ls-files`, `diff`), when not given the -z option, will quote “unusual” characters in the pathname by enclosing the pathname in a double-quote pair and with backslashes the same way strings in C source code are quoted. If this variable is set to false, the bytes higher than 0x80 are not quoted but output as verbatim. Note that double quote, backslash and control characters are always quoted without -z regardless of the setting of this variable.

### core.eol

Sets the line ending type to use in the working directory for files that have the text property set. Alternatives are *lf*, *crlf* and *native*, which uses the platform’s native line ending. The default value is native. See `gitattributes(5)` for more information on end-of-line conversion.

### core.safecrlf

If true, makes Git check if converting CRLF is reversible when end-of-line conversion is active. Git will verify if a command modifies a file in the work tree either directly or indirectly. For example, committing a file followed by checking out the same file should yield the original file in the work tree. If this is not the case for the current setting of core.autocrlf, Git will reject the file. The variable can be set to “warn”, in which case Git will only warn about an irreversible conversion but continue the operation.

CRLF conversion bears a slight chance of corrupting data. When it is enabled, Git will convert CRLF to LF during commit and LF to CRLF during checkout. A file that contains a mixture of LF and CRLF before the commit cannot be recreated by Git. For text files this is the right thing to do: it corrects line endings such that we have only LF line endings in the repository. But for binary files that are accidentally classified as text the conversion can corrupt data.

If you recognize such corruption early you can easily fix it by setting the conversion type explicitly in .gitattributes. Right after committing you still have the original file in your work tree and this file is not yet corrupted. You can explicitly tell Git that this file is binary and Git will handle the file appropriately.

Unfortunately, the desired effect of cleaning up text files with mixed line endings and
