# First Scenario: Private Files

In this scenario, a user wants to keep his or her files private. Groups are not really relevant here: it is sufficient to remove read, write, and execute permissions for others. The permissions for the group don't really matter, since in Red Hat Linux the primary group is assigned to its primary user only. Thus, a directory with its permissions set as below guarantees privacy of its contents – that is, the directory's content can't be read, written, or executed by users other than the owner:

![](bbox=[0.32, 0.25, 0.72, 0.63])

Once again, it is important to note that group permissions (Read, Write, Execute) are safe because the group in question is the group called eziudm – and the only member of this group is the user called eziudm.

# Second Scenario: Public Read-only Files

This scenario is quite simple to implement. We want to give public access to the file, and we want this public access to be read-only. Therefore, all we need to do is to ensure that the Write permission for Others is denied: