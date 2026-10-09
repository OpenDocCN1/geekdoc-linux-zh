# ## ACTIVITY 9-6
## Customizing Systems Using Variables

**Before You Begin:**
The login screen of the first CLI terminal is displayed.

**Scenario:**
As an administrator, you need to set up Linux systems for new employees. Before the completion of the setup process, you have to customize the systems with the following details:

+   - The command prompt should reflect the company name.
- The Filltimecard script should be assigned a local path on the system.
- The command history should display the last 100 entries.

| What You Do | How You Do It |
| :--- | :--- |
| **1.** Set the command prompt to reflect your company name. | a. Log in as **root**.<br><br>b. Enter `vim ~/.bashrc` to open the `~/.bashrc` file.<br><br>c. On a new line, enter `PS1=" [ Our Global Company \u ] "` to change the primary prompt. |
| **2.** Set the file path and the history file size. | a. Enter `PATH=$PATH:/root` to assign the path, where the Filltimecard script is located, to the **PATH** variable.<br><br>b. Enter `HISTSIZE=100` to assign a value of 100 to the history file content. |
| **3.** Export the variables and save the changes made to the file. | a. Type `export PS1 PATH HISTSIZE` to export the three variables.<br><br>b. Switch to the command mode.<br><br>c. Save and close the file. |