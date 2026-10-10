![](bbox=[0.11, 0.06, 0.61, 0.33])

Figure 7-8 The View Effective Rights window

+   d. Record the effective All Attributes Rights for the EKenton user:

+   e. Click the **Entry Rights** option and record the entry rights for the EKenton user:

+   f. Click **Done** to return to the iManager main window.

+   8. Repeat Step 7 to record effective rights for KThiele:

Effective All Attribute Rights:

Effective Entry Rights:

+   9. Leave iManager open for the next activity.

# Trustee Assignment to a Container

When all users in a container need the same effective rights to an object, the best solution is to make the container a trustee of that object and assign the necessary rights to the container. As in the file system, when a container is made a trustee of an object, all users in that container have the entry and attribute rights granted to the container added to their effective rights. In addition, when a container is made a trustee of another object, all subcontainers inherit the same entry and attribute rights.

A good example of using a container trustee assignment is granting rights to a Directory Map object. As you learned in Chapter 4, a Directory Map object contains a Path property that points to a directory in the file system. By reading the directory path from the Path property, client computers can use a Directory Map object to map a drive letter to a directory in the file system. (You learn how to map drive letters with Directory Map objects in Chapter 9.) As a result, to use a Directory Map object, users must have the Read right to the Directory Map object's Path property.

Eric Kenton wants to create a Directory Map object so that all users can access a shared directory in the CORP volume. To do this, he plans to create a Directory Map object in the UAS Organization and then give the UAS container rights to read the Path property, as shown in Figure 7-9. Because the entire UAS structure is treated as a single unit, rights granted to the UAS Organization also belong to users in all subcontainers. In this way, all users in the IT, Engineering, Mgmt, and Mfg OUs have rights to use the Directory Map object to access the SharedData directory on the CORP volume. In the following activity, you use ConsoleOne to make trustee assignments to a Directory Map object and then check effective rights for users in the IT OU.