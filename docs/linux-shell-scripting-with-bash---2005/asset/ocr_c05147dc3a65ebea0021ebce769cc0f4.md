# Glo bal Declarations

All declarations that apply to the entirety of the script should occur at the top of the script, beneath the header. By placing *glo bal declarations* in one place, you make it easy for someone to refer to them while reading the script

```
# Glo bal Declarations
declare -rx SCRIPT=$({0#*)})	# SCRIPT is the name of this script
declare -rx who=" /usr/bin/who"	# the who command - man 1 who
declare -rx sync="/bin/sync"	# the sync command - man 1 sync
declare -rx wc="/usr/bin/wc"	# the wc command - man 1 wc
```

# Sanity Checks

The next section, *sanity checks*, protects the script from unexpected changes in the com-puter. Normally, when a command runs at the command prompt, Bash searches several directories for the command you want to run. It can't find the command, perhaps because of a spelling mistake, Bash reports an error. This kind of behavior is good for working interactively with Bash because it saves time and any mistakes are easily correct-ed with a few keystrokes.

Scripts, on the other hand, run without any human supervision. Before a script exe-cutes any statements, it needs to verify that all the necessary files are accessible. All required commands should be executable and stored in the expected locations. These checks are sometimes called *sanity checks* because they do not let the script begin its main task unless the computer is in a known, or " sane;" state. This is especially important with operating systems such as Linux that are highly customizable: What is true on one com-puter might not be true on another.

Another way of putting it is that Bash relies on runtime error checking. Most errors are only caught when the faulty statement executes. Checking for dangerous situations early in the script prevents the script from failing in the middle of a task, otherwise mak-ing it difficult to determine where the script left off and what needs to be done to con-tinue.

Sometimes system administrators unintentionally delete or change the accessibility of a file, making it unavailable to a script. Other times, changes in the environment can change which commands are executed. Malicious computer users have also been known to tamper with a person's login profile so that the commands you think you are running are not the ones you are actually using.

In the case of the sample script, you need to verify that the commands you need are where they're supposed to be and are available to the script.

```
# Sanity checks
if test -z "$BASH" ; then
```