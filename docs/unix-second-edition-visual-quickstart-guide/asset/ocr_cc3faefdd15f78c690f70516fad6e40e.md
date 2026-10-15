# Changing Your csh Prompt

Your system's default prompt might be just a dollar sign ($) or perhaps a dollar sign and date, or other information as outlined in the Setting Your csh Prompt Promptly sidebar. You can change this prompt using the following steps. You start by finding your prompt statement (Code Listing 8.21), then modifying it in your editor (Figure 8.7).

# To change your csh prompt:

+   1. grep prompt ~/.cshrc ~/.login
+   To begin, list the configuration files located in your home directory and in the /etc directory. Look through your system configuration files for your prompt statement. It'll look something like set prompt=" $ " or set prompt="hostname> ". It's likely in your .cshrc file, as shown in Code Listing 8.21.
+   The Setting Your csh Prompt Promptly sidebar will help you translate this code.
+   2. vi .cshrc
+   Use the editor of your choice to edit the configuration file with the prompt setting in it.
+   3. set prompt="$LOGNAME > "
+   Set your prompt to something more suitable, as shown in Figure 8.7.

![](bbox=[0.55, 0.1, 0.92, 0.4])

# Setting Your csh Prompt Promptly

You can set your csh prompt to contain some types of information, but not as many as the bash or zsh prompts. The following list shows you what code to use to add certain kinds of information to your prompt (as well as help you translate the code in your existing prompt):

+   - $LOGNAME shows the userid of the current user—that's you.
+   - ${cwd} shows the current working directory with a path.
+   - `uname -n`% shows the host name of the computer.

```
xmision> grep prompt ~/.cshrc ~/.login
/home/users/e/ejroy/.cshrc:if ($?USER == 0 || $?prompt == 0) exit
/home/users/e/ejroy/.cshrc:set prompt="hostname> "
/home/users/e/ejroy/.login: exit# leave user at regular C shell prompt
xmision>
```

Code Listing 8.21 The prompt statement will likely be in your .cshrc file.