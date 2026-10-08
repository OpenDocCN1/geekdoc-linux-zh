
## History List

```
martyp $ history
125 man fc
126 set | more
127 exit
128 history
129 k
130 env | more
131 set | more
132 more .profile
133 more .profile | grep rof
134 more .profile | grep vi
135 more /etc/profile | grep vi
136 set |grep edit
137 set | grep vi
138 env | grep vi
139 history
140 who
martyp $ history
```

![](img/75f39fc91296b889c0653851accdfd46_335_0.png)

Issuing `escape k` recalled the last command issued, in this case the `who` command at line 140. Each time you press `k`, the preceding `ksh` command is fetched. This is the same as pressing `escape` and the `-` (minus) key. You can specify the number of commands you wish to go back in the history list with `escape nk`, where `n` is the number of commands you want to go back in the history list. The following example shows issuing `escape 5k` to fetch the fifth command back in the history list:

```
martyp $ history
125 man fc
126 set | more
127 exit
128 history
129 k
130 env | more
131 set | more
132 more .profile
133 more .profile | grep rof
134 more .profile | grep vi
135 more /etc/profile | grep vi
136 set |grep edit
137 set | grep vi
138 env | grep vi
139 history
140 who
martyp $ set |grep edit
```

![](img/75f39fc91296b889c0653851accdfd46_335_1.png)

Issuing `escape 5k` fetched the fifth command back in the history list at line 136. This is the same as having issued `escape 5`.

You can also move forward in the history list, using `j` in the same way we used `k` to move back in the history list. Let’s issue `escape 5k` to move back five commands in the history list to line 136, and then use `escape 3j` to move forward three commands to line 139, as shown in the following example:

```
martyp $ history
125 man fc
126 set | more
127 exit
128 history
129 k
130 env | more
131 set | more
132 more .profile
133 more .profile | grep rof
134 more .profile | grep vi
135 more /etc/profile | grep vi
136 set | grep edit
137 set | grep vi
138 env | grep vi
139 history
140 history
martyp $ who
```

Issuing `escape 3j` moved us forward to line 139, which is the same as having issued `escape 3`.

We can also go back to the oldest command in the history list with `escape G`. You can go back to a specific command number from the history list with `escape nG`, where `n` is a specific command number from the history file. The following example shows issuing `escape 126G` to go back to line 126 from the history list:

```
martyp $ history
125 man fc
126 set | more
127 exit
128 history
129 k
130 env | more
131 set | more
132     more .profile
133     more .profile | grep rof
134     more .profile | grep vi
135     more /etc/profile | grep vi
136     set |grep edit
137     set | grep vi
138     env | grep vi
139     history
140     who
martyp $ set | more
```

![](img/75f39fc91296b889c0653851accdfd46_337_0.png)

You can also recall lines from the history list based on searches. If, for instance, you want to recall the most recently issued command from the history list that has in it **profile**, you would issue `/profile`, which is the slash character followed by **profile**, to get the result shown in the following example:

```
martyp $ history
125     man fc
126     set | more
127     exit
128     history
129     k
130     env | more
131     set | more
132     more .profile
133     more .profile | grep rof
134     more .profile | grep vi
135     more /etc/profile | grep vi
136     set |grep edit
137     set | grep vi
138     env | grep vi
139     history
140     who
martyp $ more /etc/profile | grep vi
```

![](img/75f39fc91296b889c0653851accdfd46_337_1.png)

Searching for the most recent occurrence of **profile** produces line 135. Many of the other searches in **vi** work at the command line. The **vi** chapter and **vi** quick reference card have more searching information in them that you may want to try at the command line.

## Editing on the Command Line Using vi Directives

After you have "fetched" the command you wish to edit or entered a command that needs editing, you can use your **vi** directives to make modifications on the command line.

![](img/75f39fc91296b889c0653851accdfd46_338_0.png)

The **ksh** puts you in input mode immediately upon fetching a command from the history list. This approach is the converse of the **vi** program that you use to edit files, which puts you in control mode by default. After you have fetched a command from the history list, you must press *escape* in order to move into control mode when using **vi** in **ksh**.

![](img/75f39fc91296b889c0653851accdfd46_338_1.png)

Let's now perform some simple modifications to commands we have fetched from the history list. We recall line number **286** from the history list with the sequence *escape* **286G**. After recalling this command, we insert *cat* at the beginning of the command with **i cat**. **i** is for insert text to the left of the current cursor position. The following example shows the result of both the fetch of line 286 and inserting **cat**:

```
martyp $ history
285       history
286       more /etc/profile | grep vi
287       who
288       whoami
289       who
290       ls -al
291       alias
292       pwd
293       ls -al /home
294       cat .profile
295       history
296       vi .profile
297       cat /etc/passwd
298       cat /etc/passwd | grep donna
299       pwd
300       history
martyp $ cat more /etc/profile | grep vi
```

You can see that `i cat` inserted `cat` at the very beginning of the line.

We can again recall line 286 and use A to append text to the very end of the line, as shown in the following example:

```
martyp $ history
285	history
286	more /etc/profile | grep vi
287	who
288	whoami
289	who
290	ls -al
291	alias
292	pwd
293	ls -al /home
294	cat .profile
295	history
296	vi .profile
297	cat /etc/passwd
298	cat /etc/passwd | grep donna
299	pwd
300	history
martyp $ more /etc/profile | grep vieditor
```

![](img/75f39fc91296b889c0653851accdfd46_339_0.png)

In this example, we used the sequence A `editor` to insert the word `editor` at the very end of the command line we had recalled.

![](img/75f39fc91296b889c0653851accdfd46_339_1.png)

We can recall this line and change `more` at the beginning of the line to `cat` by issuing the sequence `cw cat`, as shown in the following example:

```
martyp $ history
285	history
286	more /etc/profile | grep vi
287	who
288	whoami
289	who
290	ls -al
291	alias
292	pwd
293	ls -al /home
294	cat .profile
295	history
296	vi .profile
297  cat /etc/passwd
298  cat /etc/passwd | grep donna
299  pwd
300  history
martyp $ cat /etc/profile | grep vi
```

![](img/75f39fc91296b889c0653851accdfd46_340_0.png)

This changes *more* to **cat** on the command line.

To delete the word *more* without replacing it, we fetch line 286 and issue **dw**, as shown in the following example:

![](img/75f39fc91296b889c0653851accdfd46_340_1.png)

```
martyp $ history
285  history
286  more /etc/profile | grep vi
287  who
288  whoami
289  who
290  ls -al
291  alias
292  pwd
293  ls -al /home
294  cat .profile
295  history
296  vi .profile
297  cat /etc/passwd
298  cat /etc/passwd | grep donna
299  pwd
300  history
martyp $ /etc/profile | grep vi
```

If we are unhappy with the most recent command issued we can undo the command by issuing **u**, which undoes the **dw** we used to remove *more* on the command line, as shown in the following example:

```
martyp $ history
285  history
286  more /etc/profile | grep vi
287  who
288  whoami
289  who
290  ls -al
291  alias
292	pwd
293	ls -al /home
294	cat .profile
295	history
296	vi .profile
297	cat /etc/passwd
298	cat /etc/passwd | grep donna
299	pwd
300	history
martyp $ more /etc/profile | grep vi
```

![](img/75f39fc91296b889c0653851accdfd46_341_0.png)

![](img/75f39fc91296b889c0653851accdfd46_341_1.png)

![](img/75f39fc91296b889c0653851accdfd46_341_2.png)

Issuing **u** puts back the *more* that we had removed with **dw**.

You may want to try using both the **vi** commands I have covered here, as well as other commands to add, delete, change, search and replace, copy, and undo at the command line.

## Aliases in KornShell

An alias is a name that you select for a frequently used command or series of commands. Many aliases are predefined for you.

The **alias** command, without any arguments, lists all aliases. This list includes both preset aliases as well as those you have set. The following command shows the preset aliases on the system on which I am working:

```
martyp $ alias
autoload='typeset -fu'
command='command'
functions='typeset -f'
history='fc -l'
hyper1='HHLIC='/opt/local/bristol/hyperhelp/licenses/hhptc1;export HHLIC'
hyper36='HHLIC='/opt/local/bristol/hyperhelp/licenses/hhptc36;export HHLIC'
hyper83='HHLIC='/opt/local/bristol/hyperhelp/licenses/hhptc83;export HHLIC'
hyper95='HHLIC='/opt/local/bristol/hyperhelp/licenses/hhptc95;export HHLIC'
integer='typeset -i'
local=typeset
nohup='nohup'
r='fc -e -'
stop='kill -STOP'
suspend='kill -STOP $$'
martyp $
```
