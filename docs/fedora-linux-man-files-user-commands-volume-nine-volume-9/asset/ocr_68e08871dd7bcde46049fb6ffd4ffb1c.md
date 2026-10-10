# OPTIONS

enable, run <collection1> [<collection2> …] <command> [-x|—exec]

Run <command> within the environment of the given collections. Each collection contains a module file that defines how collection modifies the environment. First the environment is modified according to module files of the given collections and then <command> is executed. Control is returned back to the caller with the original environment as soon as the <command> finishes. If <command> is ‘-’ (dash) then it is read from the standard input.

If —exec is specified then function exec() will be used for command execution otherwise function system() will be used.

Note: if you use <command> consisting of multiple argunts, you either need to use quotes or the — command separator. Everything that follows the separator will be considered a command or its argument.

Note: so commands modify user environment in so way. Those commands may potentially break SCLs, as their activation also usually depends on env. modification as well. Typical examples of such commands are su and sudo. Every collection modifies the environment differently, thus more details may be found in the documentation of the particular collection.

load <collection1> [<collection2> …]

Load the given collections into current shell. The environment of current shell is modified according to module files of the collections.

unload <collection1> [<collection2> …]

Unload the given collections from current shell. The environment of current shell is returned back to the state before loading the collections.

list-collections

Lists all installed Software Collections on the system.

list-packages <collection1> <collection2> …

If a collection na is specified then list of installed packages belonging to the collection is listed.

register <path>

If <path> leads to valid SCL file structure, scl will register that as a SCL. <path> directory needs to contain module file and root directory, to be considered valid SCL. <path> needs to be an absolute path to the collection location.

deregister <collection> [-f|—force]

<collection> will no longer be considered SCL. If the <collection> was installed locally, then the use of —force is needed.i

man <collection>

Show manual page for <collection>.