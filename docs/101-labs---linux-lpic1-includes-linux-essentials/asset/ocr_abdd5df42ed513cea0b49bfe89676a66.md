Who are the user and group owners of this file? The third and fourth fields of `ls -l` tell us that. By default, it should be your own user and primary group.

# **Task 2:**

Now run:

+   - sudo chown root foo
+   - ls -l foo
+   - cat foo

You've just changed the user ownership to root, while keeping the group ownership. As the file has group- and world-read permissions, you can still see its contents.

# **Task 3:**

Now run:

+   - sudo chmod o-r foo
+   - ls -l foo
+   - cat foo

That `chmod` command removes read permissions from other. However, as you still have group ownership, you can still see the file's contents.

# **Task 4:**

Now run:

+   - sudo chmod 600 foo
+   - ls -l foo
+   - cat foo

This `chmod` command sets the permissions explicitly, to read-write for the owning user only. As that is root, we can no longer read the file.

# **Task 5:**

Finally, clean up with `sudo rm foo`

**Notes:**

Execute permissions come into play on executable files as well as directories. If a user/group cannot "execute" a directory, it cannot view the contents of said directory or any subdirectories.