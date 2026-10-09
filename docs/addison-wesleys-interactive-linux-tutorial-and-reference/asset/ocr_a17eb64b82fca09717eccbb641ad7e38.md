Using the equals sign results in what is called an “absolute” permissions assignment.

List your home directory again to be sure that the permissions for **newdir** are the same as those shown in Figure 8-1.

Figure 8-2 presents a chart similar to the one we showed you in the *Linux Made Easy CBT*. The structure of the **chmod** command is simplicity itself: (1) ***who*** the change will affect: **ugoa** (user, group, others, all); (2) ***what*** *action* you are taking: **+** **-** = (add, remove, absolute) **rwx** (permission); (3) ***which*** *file* or *directory* is affected: **filename**.

We can sum up **chmod** with three words: ***who***, ***what***, ***which***.

![](bbox=[0.14, 0.35, 0.85, 0.4])

# **Figure 8-2 Syntax of chmod Command**

In the next series of exercises, you will change the permissions of **newdir** several times. (Note that some of the resultant permissions will not make good Linux sense. The purpose of these exercises is to give you practice with **chmod**.)

+   5. Add write permission to **newdir** for the group.
+   a. Type **chmod g+w newdir**
+   Who, what, which.
+   b. Press <Enter>
+   c. List your home directory, and check your work. You should see permissions for **newdir** as shown in Figure 8-3.

![](bbox=[0.14, 0.79, 0.85, 0.83])

# **Figure 8-3 Results of Adding Write Permission to newdir for the Group**