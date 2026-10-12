| Permission Value | Explanation |
|---|---|
| 0755 | Read (r), write (w), and execute (x) permissions for the file owner, and read (r) and execute (x) permissions for everyone else. This is equivalent to 755; the number 7 is derived by adding 4 (r) + 2 (w) + 1 (x). |
| 4755 | Same as 755 in the last example, except that this file is set-UID. |
| 2755 | Similar to 755, but also sets the set-GID bit. |
| 1755 | Similar to 755, but also sets the sticky bit, formally known as the save text mode. |

# Using access strings to set permissions

The access string method of setting permissions is (supposedly) simpler than the numeric method discussed in the preceding section. Figure 8-2 shows the access string version of the permissions diagram.

| Special | User (u) | Group (g) | Others (o) |
|---|---|---|---|
| set-UID (s) | read (r) | read (r) | read (r) |
| set-GID (s) | write (w) | write (w) | write (w) |
| sticky-bit (t) | execute (x) | execute (x) | execute (x) |

All (a)

Figure 8-2 The permissions diagram using access strings.

With this method, each type of permission is represented with a single character (in parentheses). To create a permission string, you need to specify the following:

+   - **Who it affects.** Your choices are u (user), g (group), o (others), or a (all).
+   - **The type of permission that needs to be set.** Your choices are r (read), w (write), x (execute), s (set-UID or set-GID), or t (sticky bit). For more info on these choices and what they mean, see the previous section.