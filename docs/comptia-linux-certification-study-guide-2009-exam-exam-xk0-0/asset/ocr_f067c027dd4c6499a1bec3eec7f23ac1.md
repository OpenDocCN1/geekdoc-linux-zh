which is updated using `apt-get update`, to update all installed applications to their most current versions.

Incorrect answers and explanations: **A, C**, and **D**. Answer **A** is incorrect because it is the command to update the APT database. Answer **C** is incorrect because the `dist-upgrade` option upgrades the entire distribution to the latest version and the requirements in this question ask for only the installed applications to be updated. Answer **D** is incorrect because, when a package name is specified, it is the command to install an individual application.

# ## CHAPTER 8: INSTALLING, CONFIGURING AS A WORKSTATION

+   1. A user has sent three jobs to a printer, with job numbers **372**, **373**, and **374**. They now want to remove printer job number **373**, which has not been printed yet. Which command will achieve this?

+   A. `lpr --cancel 373`
+   B. `lpstat -c 373`
+   C. `cancel 373`
+   D. `lpr -c 373`

Correct answer and explanation: **C**. The correct answer is **C** as the `cancel` command will cancel the given job provided it is still in the queue and the user is the owner or has the correct permissions.

Incorrect answers and explanations: **A, B**, and **D**. Answers **A** and **D** are incorrect as the `lpr` command submits jobs to a printer. Answer **B** is incorrect as the `lpstat` command will display the status of a printer.

+   2. A user is running KDE as his display environment. What will be the most likely environment variable for the display manager?

+   A. `DISPLAYMANAGER="KDE"`
+   B. `DISPLAYMANAGER="kdm4"`
+   C. `DISPLAYMANAGER="kde_display"`
+   D. `DISPLAYMANAGER="gdm"`

Correct answer and explanation: **B**. The correct answer is **B** as this will specify version 4 of the K Display Manager.

Incorrect answers and explanations: **A, C**, and **D**. Answer **A** is incorrect as KDE is the overall K Desktop Environment and not the display manger. Answer **C** is wrong as this does not define K Display