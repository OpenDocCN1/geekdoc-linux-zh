# # KIOSK Admin Tool

# ## Menu Actions Configuration

| Action |
| --- |
| [ ] Disable File -> New
| [ ] Disable File -> Open...
| [ ] Disable File -> Recent
| [ ] Disable File -> Save...
| [ ] Disable File -> Reset
| [ ] Disable File -> Close
| [ ] Disable File -> Print Preview...
| [ ] Disable File -> Mail...
| [ ] Disable File -> Quit
| [ ] Disable File -> Edit...

Disable File -> New
This can be used to remove the File -> New menu-option from all applications.

![](bbox=[0.27, 0.093, 0.729, 0.497])

Figure 7-5 Menu actions configuration with the Kiosk Admin Tool

# ### Immutable configuration entries

As we have seen

Entries can be marked immutable on an entry, group, or file by adding [i] at the right places, as shown in Example 7-3 on page 148. If KDE does not have write access to the user's configuration files, they will automatically be considered immutable and the user will be warned about that fact. If you do not have this behavior, add `warn_unwritable_config=false` to the Action Restrictions section in /etc/kderc (or kdeglobals on the global, profile, or user level) to disable this warning for all applications. Non-writable configuration files are not a foolproof lock down mechanism because users can potentially rename these files and add new ones according to their tastes. Consider the file system mechanisms an add-on to the much more sophisticated KDE Kiosk framework.