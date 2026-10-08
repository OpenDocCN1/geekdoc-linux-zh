# Ownership and Permissions 97

The command chmod is like a smorgasbord where you can choose any combination of items from either the first or last boxes, and stick your choice from the center box between them.

For example, if you wanted to add permission to the file test for everyone in your group, you would, working backwards from that description, choose g for group, + for add, and w for write. The finished UNIX command would be chmod g+w test.

If you decided to take away and execute permission for everyone not in your group, you could use chmod -rx test to accomplish the task.

![](bbox=[0.125, 0.317, 0.193, 0.337])

+   1. Turn to your computer and, using touch and is, changing permissions and what happens.
% test
% ls -l test
-rw------- 1 taylor 0 Oct 11 18:29 test

+   2. The first modification I want to make is that people in my group should be able to read the file. Because I don't really want altering it, I will rescind-write permission for group members
% chmod g-w test
% ls -l test
-rw------- 1 taylor 0 Oct 11 18:29 test

+   3. But then boss reminds me that everyone in the group should have all access permissions for everyone in that group. Okay, I'll do so.
% chmod g-rw test
% ls -l test
-rw------- 1 taylor 0 Oct 11 18:29 test

I also could have done that with chmod g=, of course.

+   4. Wait a second. This file is just for my own use, and nobody in my group should be looking at it anyway. I'll change it back.
% chmod g-rw test
% ls -l test
-rw------- 1 taylor 0 Oct 11 18:29 test

Great, now the file is set so that I can read and write it, but nobody else touch it, read it, modify it, or anything else.

+   5. If I relented a bit, I could easily add, with one last chmod command, read-only permission for everyone:
% chmod a+r test
% ls -l test
-rw-r---- 1 taylor 0 Oct 11 18:29 test

![](bbox=[0.863, 0.571, 0.977, 0.683])