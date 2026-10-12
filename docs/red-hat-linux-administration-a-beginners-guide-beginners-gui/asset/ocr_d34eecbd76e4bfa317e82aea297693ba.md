| -g *group* | Sets the *quota* information for the named *group*. |
| -p *login* | Allows you to clone one user’s (user *login*) information to another user. Must be set in conjunction with the -u option. |

When you invoke the edquota command, it brings up the configuration information for the particular user, group, or grace period you want to add or edit. By default, the vi editor is used to display human-readable information. If you prefer another editor, such as emacs or pico, you can simply change the EDITOR environment variable before running edquota. For example, if you’re using BASH (the root user’s default shell), you would enter this command:

```
`[root@tedford]# export EDITOR=pico`
```

Once the edquota information is on screen, you can edit it, save the document, and quit. The edquota process takes that information and places it into the database. Note that edquota uses the /etc/passwd file to determine the location of a user’s home directory.

# ### Examples of edquota

To place a quota on user blee, I would use the following command:

```
`[root@tedford]# edquota -u blee`
```

This will bring up the editor with a file that looks like the following:

> > Quotas for user blee:
> > /dev/hda2: blocks in use: 0, limits (soft = 0, hard = 0)
> > inodes in use: 0, limits (soft = 0, hard = 0)

Zeros in all the limits means there is no quota on blee’s account at the moment. Notice that there is a limit value for i-nodes as well as blocks. Remember that one block is equal to 1K under Linux, and i-nodes are the control information needed to store files. You will usually need only a few i-nodes per file, and more as the file grows larger.

So to set blee’s soft block limit to 5000, the hard block limit to 6000, the soft i-node limit to 2500, and the hard i-node limit to 3000, I would edit the file to look like this:

> > Quotas for user blee:
> > /dev/hda2: blocks in use: 0, limits (soft = 5000, hard = 6000)
> > inodes in use: 0, limits (soft = 2500, hard = 3000)

![](bbox=[0.14, 0.83, 0.45, 0.88])

The edquota command generates a unique name for the temporary file used to edit this information. Keep this file—do not write over the quota.user or quota.group file with this information! The edquota utility will take care of integrating quota information into those two files for you.