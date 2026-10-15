+   - **w.** Allows the program to have write access to the resource. Files must have this permission if they are to be unlinked (removed).
+   - **l.** Link mode mediates access to symlinks and hardlinks and grants the privilege to unlink (remove) files.
+   - **m.** Allow executable mapping. This mode allows a file to be mapped into memory using mmap(2)'s PROT_EXEC flag. This flag marks the pages executable; it is used on some architectures to provide non-executable data pages, which can complicate exploit attempts. AppArmor uses this mode to limit which files a well-behaved program (or all programs on architectures that enforce non-executable memory access controls) may use as libraries, to limit the effect of invalid -L flags given to ld(1) and LD_PRELOAD, LD_LIBRARY_PATH, given to ld.so(8).
+   - **ix.** Inherit Execute Mode. The executed resource inherits the current profile.
+   - **px.** Discrete Profile Execute Mode. This mode requires that a profile be defined for the resource executed. If there is no profile defined, access is denied.
+   - **Px.** Discrete Profile execute mode -- scrub the environment. Px allows the named program to run in px mode, but AppArmor will invoke the Linux Kernel's unsafe_exec routines to scrub the environment, similar to setuid programs. (See man 8 ld.so for some information on setuid/setgid environment scrubbing.)
+   - **ux.** Unconstrained Execute Mode. Allows the program to execute the resource without any Novell AppArmor profile being applied to the executed resource. *This should only be used in rare exceptions.*
+   - **Ux.** Unconstrained execute -- scrub the environment. As ux, it should only be used in rare exceptions.

The last five, ix, px, Px, ux, and Ux, cannot be combined.

The manual page covering the syntax of the profiles is
**man 5 apparmor.d**