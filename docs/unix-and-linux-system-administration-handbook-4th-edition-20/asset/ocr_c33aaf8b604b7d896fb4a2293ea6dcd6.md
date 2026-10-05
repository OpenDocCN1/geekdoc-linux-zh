# NFS4 ACL viewing in Solaris

# ACL inheritance

Like POSIX ACLs, NFSv4 ACLs allow newly created objects to inherit access controls from their enclosing directory. However, the NFSv4 system is a bit more powerful and a lot more confusing. Here are the important points:

+   * Any ACE can be flagged as inheritable. Inheritance for newly created subdirectories (dir_inherit or d) and newly created files (file_inherit or f) are flagged separately.

+   * You can apply different access controls to files and directories by creating separate access controls on the parent directory and flagging them appropriately. You can also apply a single ACE to all new child entities (of whatever type) by turning on both the d and f flags.

+   * From the perspective of access determination, access controls have the same effect on the parent (source) directory whether or not they are inheritable. If you want an entry to apply to children but not the parent directory itself, turn on the ACE's inherit_only (i) flag.

+   * New subdirectories normally inherit copies of each ACE: one with the inheritance turned off, which applies to the subdirectory itself; and one with the inherit_only flag turned on, which sets up the subdirectory to propagate its inherited ACEs. You can suppress the creation of this ACE by turning on the no_propagate (n) flag on the parent directory's copy of the ACE. The result is that the ACE propagates only to immediate children of the original directory.

+   * Don't confuse the propagation of access controls with true inheritance. Your setting an inheritance-related flag on an ACE simply means the ACE will be copied to new entries. It does not create any ongoing relationship between the parent and its children. If you later change the ACE on the parent directory, the children are not updated.

Table 6.10 NFSv4 ACE inheritance flags

| Code | Verbose name | Meaning |
|---|---||
| f | file_inherit | Propagate this ACE to newly created files |
| d | dir_inherit | Propagate this ACE to newly created subdirectories |
| i | inherit_only | Propagate, but don't apply to the current directory |
| n | no_propagate | Propagate to new subdirectories, but not their children |

NFSv4 ACL viewing in Solaris

Solaris has integrated its ACL support into ls and chmod, which is a nice proach and a straightforward extension of the commands' usual functions.