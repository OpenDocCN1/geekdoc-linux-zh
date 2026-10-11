```
return -EACCES;
if (!inode->i_sb)
return -EACCES;
if ((retval = permission(inode, MAY_EXEC)) != 0)
return retval;
/* better not execute files which are being written to */
if (atomic_read(&inode->i_writecount) > 0)
return -ETXTBSY;

bprm->e_uid = current->euid;
bprm->e_gid = current->egid;
id_change = cap_raised = 0;

/* Set-uid? */
if (mode & S_ISUID) {
bprm->e_uid = inode->i_uid;
if (bprm->e_uid != current->euid)
id_change = 1;
}

/* Set-gid? */
/*
 * If setgid is set but no group execute bit then this
 * is a candidate for mandatory locking, not a setgid
 * executable.
 */
if ((mode & (S_ISGID | S_IXGRP)) == (S_ISGID | S_IXGRP)) {
bprm->e_gid = inode->i_gid;
if (!in_group_p(bprm->e_gid))
id_change = 1;
}

/* We don't have VFS support for capabilities yet */
cap_clear(bprm->cap_inheritable);
cap_clear(bprm->cap_permitted);
cap_clear(bprm->cap_effective);

/*  To support inheritance of root-permissions and suid-root
 *  executables under compatibility mode, we raise the
 *  effective and inherited bitmasks of the executable file
 *  (translation: we set the executable "capability dumb" and
 *  set the allowed set to maximum). We don't set any forced
 *  bits.
 *
 *  If only the real uid is 0, we only raise the inheritable
 *  bitmask of the executable file (translation: we set the
 *  allowed set to maximum and the application to "capability
 *  smart").
 */

if (!issecure(SECURE_NOROOT)) {
if (bprm->e_uid == 0 || current->uid == 0)
cap_set_full(bprm->cap_inheritable);
if (bprm->e_uid == 0)
```