text; then press Esc to exit insert mode. To save and quit, type a colon followed by **wq** and press Enter.

When programming we tend to use a sandbox subdirectory in our home directory where we keep all sorts of temporary files that we were just playing around with. We can use a personal job to empty that directory every morning at 6 a.m. so that we get a fresh start each morning. Here is how that would look in our crontab file:

```
0 6 * * * rm -rf /home/paul/sandbox/*
```

If you are not allowed to schedule jobs, you will be stopped from editing your crontab file.

When your jobs are placed, you can use the command crontab -l to list your jobs. This just prints the contents of your crontab file, so its output is the same as the line you just entered.

If you want to remove just one job, the easiest thing to do is type crontab -e to edit your crontab file in vim; then, after having moved the cursor to the job you want to delete, type dd (two ds) to delete that line. If you want to delete all your jobs, you can use crontab -r to delete your crontab file.

# ## Basic Shell Control

Fedora includes a rich assortment of capable, flexible, and powerful shells. Each shell is different but has numerous built-in commands and configurable command-line prompts and might include features such as command-line history, the capability to recall and use a previous command line, and command-line editing. As an example, the bash shell is so powerful that it is possible to write a minimal web server entirely in bash's language using 114 lines of script (see the link at the end of this chapter).

Although there are many shells to choose from, most people stick with the default, bash. This is because bash does everything most people need to do, and more. Change your shell only if you really need to.

Table 15.1 lists each shell, along with its description and location, in your Fedora file system.

**TABLE 15.1 Shells with Fedora**

| Name | Description | Location |
| :--- | :--- | :--- |
| ash | A small shell (sh-like) | /bin/ash |
| ash.static | A version of ash not dependent on software libraries | /bin/ash.static |
| bash | The Bourne Again Shell | /bin/bash |
| bsh | A symbolic link to ash | /bin/bsh |
| csh | The C shell, a symbolic link to tcsh | /bin/csh |
| ksh | The Korn shell | /bin/ksh, /usr/bin/ksh |
| pdksh | A symbolic link to ksh | /usr/bin/pdksh |