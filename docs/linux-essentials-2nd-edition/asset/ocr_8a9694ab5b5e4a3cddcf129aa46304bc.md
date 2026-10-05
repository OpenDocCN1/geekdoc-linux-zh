# Chapter 14 • Setting Ownership and Permissions

![](bbox=[0.248, 0.105, 0.811, 0.477])

FIGURE 14.1 Linux file managers give you access to the file's ownership and permission metadata.

You should be extremely cautious about running Nautilus as root. If you forget that you're running this program as root, you can easily create new files as root, which will require additional root-privilege actions to correct by changing file ownership. It's also easy to delete critical system files accidentally as root, which you could not delete as an ordinary user. For these reasons, we recommend that you use a text-model shell to adjust file ownership. The change in the prompt makes it easier to notice that you're running as root, and if you're used to use a GUI, you're less likely to launch additional programs as root from a text-mode shell than from Nautilus.

Certification Objective

# Setting Ownership in a Shell

The command to change the ownership of a file in the preferred text-mode manner is chown. In its most basic form, you pass the name of a file followed by a username:

The chown command stands for change owner.

```
# chown bob targetfile.edf
```