That said, you must be running at securelevel −1 to unset many flags. So, without further ado, let’s discuss securelevels and what they mean to you.

# ## Securelevels

Securelevels are kernel settings that change basic system behavior to disallow certain actions. The kernel behaves slightly differently as you raise the securelevel. For example, at low securelevels, file flags can be removed. A file might be flagged immutable—but you can remove the flag, edit the file, and reflag it. When you increase the securelevel, the file flag can’t be removed. Similar changes take place in other parts of the system. Taken as a whole, the behavior changes that result from increased securelevels either frustrate or stop an intruder. Enable securelevels at boot with the `rc.conf` option `kern_securelevel_enable="YES"`.

Securelevels complicate system maintenance by imposing restrictions on your behavior. After all, many system administration tasks are also things intruders might do to cover their tracks. For example, at certain securelevels, you can’t format or mount new hard drives while the system is running. On the other hand, securelevels hamper intruders even more than they hamper you.

# ## Securelevel Definitions

Securelevels come in 5 degrees: −1, 0, 1, 2, and 3, with −1 being the lowest and 3 the highest. Once you enable securelevels with the `kern_securelevel_enable` `rc.conf` option, you can set the securelevel at boot with the `kern_securelevel` `rc.conf` variable. You can raise the securelevel at any time, not just at boot, but you can’t lower it without rebooting into single-user mode. After all, if you could lower the securelevel at any time, so could your intruder!

The effects of each securelevel vary depending on your FreeBSD release. To get the latest information, read security(7).

# ### Securelevel −1