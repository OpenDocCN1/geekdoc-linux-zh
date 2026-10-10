# File System Security Guidelines

To help keep file system security as simple and effective as possible, Novell suggests that CNAs follow certain guidelines. In this section, you learn how the Novell-recommended guidelines can be used to improve your file system security plan.

# Identify Rights Needed for Each User

The first guideline in establishing file system security successfully is to analyze each user's processing needs and then determine and document the access rights each directory needs to meet processing requirements. An advantage of this analysis is that you can identify processing needs that are common to multiple users, which reduces and simplifies the number of trustee assignments you need to make. When several users need the same rights to a set of files, it's much easier to keep track of and maintain a single trustee assignment to a group or container than to make the same trustee assignments repeatedly for several users.

# Proper Directory Structure Design

A proper directory design takes advantage of the principle that lower-level directories and files inherit rights from higher-level directories—a top-down inherited rights strategy. Planning a directory structure is the key to taking advantage of this top-down strategy and preventing users from inheriting rights to directories in which they don't belong. The following list of suggestions can help you set up a top-down strategy:

+   - Design a directory structure with directories requiring the most security near the top of the structure, separated from the directories that allow general user access. A well-designed directory structure can help reduce the number of trustee assignments by using the inherited rights principle so that a common set of rights flows down to subdirectories. A good example of this strategy is the UAS Apps directory structure, which has subdirectories for all software packages available to users.
+   - Directories that limit access to specific users or access rights shouldn't be included in a directory structure that has a trustee assignment for other users. For example, a document directory shouldn't be included in an application directory unless you want all application users to be able to read the documents.
+   - Use IRFs to protect high-security directories against inheriting unwanted trustees accidentally. An IRF is a good way to prevent effective rights from flowing into the directory from a parent directory accidentally.

# Reduce Use of IRFs

The need for an IRF as part of your security plan might indicate that you have placed a directory needing more security within a general-purpose directory, and you need to rethink your directory structure design. For example, the file system on a server in your company has a directory structure like the one in Figure 6-12. The budget files are stored in a subdirectory of the Apps SP directory, and the root of the tree has been made a trustee of Apps with Read and File Scan rights. Because [R:O], a trustee of Apps with [R: F] rights, all users inherit [R: F] rights to the Budgets subdirectory, creating a potential security problem in which all users have rights to read the budget data.

To prevent this security problem, you could block inherited rights by removing all rights from the Budgets subdirectory's IRI, giving rights to only the Accounting group, which is a trustee of the Budgets subdirectory. Although this solution works, it doesn't address the real problem of placing a subdirectory with higher security needs within a general-purpose directory. A better solution is to move the Budgets subdirectory to a secure location in the file system and then make the appropriate trustee assignments, as shown in Figure 6-13.

Another method many network administrators use is reducing the number of IRFs whenever possible to use an explicit trustee assignment for reducing a user or group's effective rights. In addition, troubleshooting explicit trustee assignments is usually easier than tracing IRFs.