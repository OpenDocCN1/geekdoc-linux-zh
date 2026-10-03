# APPLY YOUR KNOWLEDGE

E. Use the ACL mechanism to give the user RW access to each crontab table.

8. Which command(s) grants a user access to a role account?

+   - A. roleadd
- B. rolemod
- C. useradd
- D. usermod

9. Which option to the rolemod command appends an authorization to an exiting list of authorizations?

+   - A. -A
- B. -P
- C. -a
- D. -o
- E. None

10. In which files are profiles defined?

+   - A. prof_attr
- B. user_attr
- C. exec_attr
- D. auth_attr

11. What statements are true regarding the following line:

```
Media Restore:suser:cmd:::/usr/lib/fs/ufs/ufsrestore:euid=0
```

+   - A. It represents a profile in the exec_attr database.
- B. Any role that has Media Restore as a profile is able to execute the ufsrestore command with an effective UID of root.

+   - C. It represents a profile in the prof_attr database.
- D. It represents a role definition in the user_attr database.

12. In RBAC, which of the following is a bundling mechanism for grouping authorizations and commands with special attributes?

+   - A. Profile
- B. Role
- C. Authorization
- D. Group

# Answers to Review Questions

1. A., B. The roleadd command looks very similar to the useradd command, and it uses the same default shell as the useradd command.

2. A. user_attr (extended user attributes database) associates users and roles with authorizations and profiles.

3. D. exec_attr (profile attributes database) defines the privileged operations assigned to a profile.

4. D. Four valid keys exist: euid, uid, egid, and gid.

5. A. If a role is not associated with a correct profile, the only commands that can be executed within the role are the privileged commands that you have set up. Ordinary non-privileged commands are unavailable.

6. B., C., D. The three files that RBAC uses are /etc/user_attr, /etc/security/exec_attr, and /etc/security/prof_attr.