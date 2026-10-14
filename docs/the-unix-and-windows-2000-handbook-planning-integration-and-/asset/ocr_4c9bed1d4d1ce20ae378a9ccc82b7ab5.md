/etc/resolv.conf file and that DNS is functioning correctly on the NIS+ server.

# Merging NIS+ Domains

If you are in an older environment or you acquire other NIS+ domains, you may be asked to merge your NIS+ database with another already established domain. While on the surface this may sound simple, the process of merging NIS+ domains isn’t as simple as it sounds. You can’t just take all the files, concatenate them together, and expect to have a working NIS+ server!

> Merging two or more NIS+ databases is actually more difficult than creating one from scratch. You need to examine each database element to look for duplication.

Merging two or more NIS+ databases is actually exponentially more difficult than creating one from scratch. You need to examine each database element to look for duplication. You also may have stylistic differences that will require you to re-create information. When looking to merge NIS+ environments, make sure to:

+   - Check the passwd files for duplicate usernames and user IDs (UIDs). This is perhaps the most difficult part of merging NIS+ domains. Users are very protective of their identities, and if you have duplication, it may be difficult to coax one user to change their identity. Be courteous and understanding, and explain why the change is necessary. Of course, if understanding and compassion don’t do the trick, make sure you let the person with the most authority keep their username unaltered!
+   - Given that you have to make UID changes, make sure you scan all filesystems on which that user may have owned files. Otherwise, you may leave files owned by a non-associated UID, or even worse, you may inadvertently grant ownership of files to another user.
+   - If you use NIS+ for hostname resolution, scan for duplicate hostnames. Just about every installation has a mars.yourdomain.com or elvis.yourdomain.com, so you’ll need to motivate someone to change their hostname. This can be simple or difficult, depending on the complexity of the systems involved. Here it may not be wise to give the users a choice. You may just want to rename the server with the least amount of third-party software, network services, or user home directories. If you employ automounting, make sure you make the necessary changes there, as well as in any netgroup files.