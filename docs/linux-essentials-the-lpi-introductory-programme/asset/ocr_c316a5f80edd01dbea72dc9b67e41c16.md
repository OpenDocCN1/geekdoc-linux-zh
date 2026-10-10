# Table 5.1: Manual page sections

| Section | Content |
|:---|:---|
| NAME | Command name and brief description |
| SYNOPSIS | Description of the command syntax |
| DESCRIPTION | Verbose description of the command’s effects |
| OPTIONS | Available options |
| ARGUMENTS | Available Arguments |
| FILES | Auxiliary files |
| EXAMPLES | Sample command lines |
| SEE ALSO | Cross-references to related topics |
| DIAGNOSTICS | Error and warning messages |
| COPYRIGHT | Authors of the command |
| BUGS | Known limitations of the command |

Here, (*name*) is the command or file name that you would like explained. “*man bash*”, for *example*, produces a list of the abovementioned internal shell commands.

However, the manual pages have some disadvantages: Many of them are only available in English; there are sets of translations for different languages which are often incomplete. Besides, the explanations are frequently very complex. Every single word can be important, which does not make the documentation accessible to beginners. In addition, especially with longer documents the structure can be obscure. Even so, the value of this documentation cannot be underestimated. Instead of deluging the user with a large amount of paper, the on-line manual is always available with the system.

> Many Linux distributions pursue the philosophy that there should be a manual page for every command that can be invoked on the command line. This does not apply to the same extent to programs belonging to the graphical desktop environments KDE and GNOME, many of which not only do not come with a manual page at all, but which are also very badly documented even inside the graphical environment itself. The fact that many of these programs have been contributed by volunteers is only a weak excuse.

# ### 5.3.2 Structure

The structure of the man pages loosely follows the outline given in Table 5.1, even though not every manual page contains every section mentioned there. In particular, the EXAMPLES are frequently given short shrift.

> The BUGS heading is often misunderstood: Read bugs within the implementation get fixed, of course; what is documented here are usually restrictions which follow from the *approach* the command takes, which are not able to be lifted with reasonable effort, and which you as a user ought to know about. For example, the documentation for the *grep* command points out that various constructs in the regular expression to be located may lead to the *grep* process using very much memory. This is a consequence of the way *grep* implements searching and not a trivial, easily fixed error.

Man pages are written in a special input format which can be processed for text display or printing by a program called *groff*. Source code for the manual pages is stored in the */usr/share/man* directory in subdirectories called *man$n*, where *n* is one of the chapter numbers from Table 5.2.

> You can integrate man pages from additional directories by setting the *MANPATH* environment variable, which contains the directories which will be searched by *man*, in order. The *manpath* command gives hints for setting up *MANPATH*.