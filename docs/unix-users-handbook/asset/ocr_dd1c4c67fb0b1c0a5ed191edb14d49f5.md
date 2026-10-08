![](bbox=[0.2, 0.1, 0.8, 0.55])

**Figure 16-12**  Viewing the Properties of **install.vars**

**install.vars** is *Read-only* because this file is owned by *root* on the UNIX system and not by user *hp*, which is the UNIX user under which we mounted /home/hp.

We are unable to *Chmod*, or modify the permissions on this file, because it is owned by *root* and we have mounted /home/hp as the user *hp*, as shown in Figure 16-13.