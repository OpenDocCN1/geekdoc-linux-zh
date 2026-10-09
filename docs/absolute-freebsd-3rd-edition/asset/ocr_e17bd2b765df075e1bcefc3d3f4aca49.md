| own | da20 | xistence:xistence |
| :--- | :--- | :--- |

This might not have the desired effect, however, as some programs still think that you must be root to carry out operations on devices. I've seen more than one piece of software shut itself down if it's not run by root, without even trying to access its device nodes. Changing the device node permissions won't stop those programs' complaints when they're run by a regular user.

Configuration with devfs.conf(5) solves many problems, but not all. If you want a device node to simply be invisible and inaccessible, you must use devfs rules.

# # Global devfs Rules

Every devfs(5) instance behaves according to the rules defined in devfs.rules. The devfs rules apply to both devices present at boot and devices that appear and disappear dynamically. Rules allow you to set ownership and permissions on device nodes and make device nodes visible or invisible. You cannot create symlinks to device nodes with devfs rules.

Similar to /etc/rc.conf and /etc/defaults/rc.conf, FreeBSD uses /etc/devfs.rules and /etc/defaults/devfs.rules. Create an /etc/devfs.rules for your custom rules and leave the entries in the defaults file alone.

# ## devfs Ruleset Format

Each set of devfs rules starts with a name and a ruleset number between square brackets. For example, here's a devfs rule from the default configuration:

```
```python
[@devfsrules_hide_all=@1]
@add hide
```
```

The first rule in devfs.rules is called devfs_hide_all ① and is ruleset number 1 ②. This ruleset contains only one rule ③.