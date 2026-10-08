# CHAPTER 7 | Networks, Firewalls, and More 213

| TABLE 7-3 AppArmor access modes |
| MODE | DESCRIPTION |
| r | Read |
| w | Write (cannot use with append) |
| a | Append (cannot use with write) |
| ux | Execute, in unconfined mode |
| Ux | Execute, in unconfined mode, supports unconfined child processes |
| px | Profile execute mode, works only if related files/commands also have AppArmor profiles |
| Px | Profile execute mode, works only if related files/commands also supports unconfined child processes |
| ix | Inherit execute mode; inherits the current profile |
| m | Maps to an executable file |
| l | Allows links to other files |
| k | Supports file locks |

# AppArmor Configuration and Management Commands

There are several AppArmor commands. The apparmor_status command, as described earlier, lists configured profiles of commands and services, along with their enforce modes. Additional AppArmor commands start with aa- and reside mostly in the /usr/sbin/ directory. The purpose of each command is described in Table 7-4.

# An AppArmor Configuration Tool

If you need a graphical tool to configure AppArmor, it's available on SUSE Linux. While it is not one of the distributions covered in this book, SUSE Linux is an excellent distribution with enterprise-quality support, courtesy of Novell. Figure 7-8 illustrates a step in SUSE's AppArmor configuration wizard, avoidable through its YaST package. Those of you familiar with SUSE will recognize the console version of the tool, which is a low-level graphics version of that can be used remotely without a GUI.