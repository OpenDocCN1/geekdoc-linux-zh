
## Part I: Exercise Instructions (Continued)

1.  Upload a file to the shared folder:
    - e. Select (highlight) the **shared** folder.
    - f. In the right pane, select **File > Upload**.
    - g. In the Upload File window, select **Browse**.
    - h. Browse to `C:\Documents and Settings\All Users\Shared Documents\Shared Pictures\Sample Pictures`.
    - i. Select **Blue hills**; then select **Open**.
    - j. From the Upload File window, select **Upload**.

2.  Verify that the file was uploaded to the NNLS server:
    - a. At the NNLS server, open a *terminal session*.
    - b. Enter `su -`; then enter `novell` for the password.
    - c. Enter `cd /var/opt/novell/netstorage/shared`.
    - d. Enter `ls -l Blue*`.
    - You should see the Blue hills.jpg file listed.

3.  Create a personal storage location for the team lead from the team lead's home directory:
    - a. On your NNLS server, from iManager under **File Access (NetStorage)**, select **Storage Location: Create**.
    - b. In the Object Name field, enter **TeamLead**.
    - c. In the Display name field, enter **TeamLead**.
    - d. In the Directory Location field, enter `cifs://10.0.0.x/SRife`.
    - e. In the Context field, enter *your container*.
    - f. Select **Create**.
    - g. When prompted that the location was created, select **OK**.

4.  Associate the new storage location with SRife by completing the following:
    - a. Select **Storage Location: Create / Modify List**.
    - b. In the Object field, browse to and select **SRife**.
    - c. Select **OK**.
    - d. In the *Storage Location Objects* field, browse to and select **TeamLead_your_container**, then select **OK**.
    - e. When prompted that the assignment succeeded, select **OK**.

5.  Verify that the **TeamLead** storage location object is available to **SRife** by logging in to NetStorage as **SRife**:
    - a. In Mozilla, select *File > New > Navigator Window* to open a new browser window.
    - b. Enter *https://your_server_DNS/NetStorage*.
    - c. When prompted, authenticate as **SRife** with a password of **novell**, then select **OK**.
    - You should see the TeamLead storage location displayed.

6.  Attempt to view files in, and upload files to, the TeamLead folder:
    - a. Select the **TeamLead** folder.
    - The right pane will be blank if you have not converted SRife to a LUM and Samba user.
    - b. From the NetStorage menu, select *File > Upload*.
    - The Upload window will also be blank because SRife is not a LUM and Samba user.
    - c. Log out of NetStorage, by selecting *Logout*.

### Part II: Configure the Team Lead to Use a Personal Folder

In this part of the exercise you will configure SRife to use the personal folder you created for him. You will also verify that other users cannot see the TeamLead folder.

To accomplish this, do the following:

1.  Using steps that you have already performed in previous exercises, convert **SRife** to LUM and Samba. Use the following information:
    - Primary group: **ACCTUSERS**
    - Samba password: **novell**

2.  Log in as a LUM user to create SRife's *home directory*.

3.  On your NNLS server, log into NetStorage as **SRife**.

4.  View the files in SRife's TeamLead folder, by selecting **TeamLead**.
    - You should see the default files and folders created in SRife's home directory.

5.  Upload a file to the TeamLead folder:
    - a. Select **File > Upload**.
    - b. From the Upload File window, select **Browse**.
    - c. Browse to **/tmp**.
    - d. Select *your container*.ldif, then select **Open**.
    - e. From the Upload File window, select **Upload**.
    - The NetStorage screen refreshes and the *your container*.ldif file appears in the list of files in the TeamLead folder.
    - f. Log out of NetStorage by selecting **Logout**.

6.  Convert **JNelso**, who is already a LUM user, to a Samba user.

7.  Log in to NetStorage as **JNelson** and attempt to view the TeamLead folder.
    - Although JNelson is a Samba user, she cannot see the TeamLead folder because she is not assigned to the TeamLead storage location object. She also does not have rights to SRife's home directory.

8.  Log out as **JNelson**.

9.  **Close** the browser window.

### Part III: Create a Project Files Folder the Team Can Use to Share Files

In this part of the exercise you will configure storage location objects to point to a public share that everyone in your container can use and to a private share that only the team can use to share files.

To accomplish this, do the following:

1.  Create a Storage Location:
    - a. From iManager under **File Access (NetStorage)**, select **Storage Location: Create**.
    - b. In the Object Name field, enter **PublicShare**.
    - c. In the Display name field, enter **PublicShare**.
    - d. In the Directory Location field, enter `cifs://10.0.0.x/tmp`. The `/tmp` directory was configured as a public Samba share in a previous exercise.
    - e. In the Context field, enter *your container*.
    - f. Select **Create**.
    - g. When prompted that the location was created, select **OK**.

2.  Associate the new storage location with the ACCTUSERS group by completing the following:
    - a. Select **Storage Location: Create / Modify List**.
    - b. In the Object field, browse to and select *your container*.
    - c. Select **OK**.
    - d. In the Storage Location Objects field, browse to and select *PublicShare.your container*; then select **OK**.
    - e. When prompted that the assignment succeeded, select **OK**.

3.  Test the configuration by completing the following:
    - a. In Mozilla, select *File > New > Navigator Window* to open a new browser window.
    - b. Enter `https://your_server_DNS/NetStorage`.
    - c. When prompted, authenticate as **kfullner** with a password of **novell**; then select **OK**.
    - You should see the PublicShare storage location displayed. You cannot see any files in the PublicShare folder because kfullner has not been converted to a Samba user.
    - d. Select the **Logout** icon on the NetStorage menu bar.

4.  Convert **kfullner** to LUM and Samba and attempt again to log in as kfullner and access the PublicShare folder; then **logout** and close the browser window.

5.  Prepare a directory on your NNLS server where files for a project team can be saved by completing the following:
    - a. On your NNLS server, create a new directory in `/var` called ProjectFiles by entering `mkdir /var/ProjectFiles`.
    - b. Assign ACCTUSERS as Group for `/var/ProjectFiles`, by entering `chown root:ACCTUSERS /var/ProjectFiles`.
    - ACCTUSERS is already a LUM group. If it has not been converted to LUM you will receive an error at this point.
    - c. Give Group **rwx** permissions to the directory and restrict root and Others from having permissions by entering `chmod 070 /var/ProjectFiles`.

6.  Edit `smb.conf` to create a private Samba share that gives ACCTUSERS access, through Samba, to the ProjectFiles folder:
    - a. Select **Applications > KDE Menu > System > File Manager - Super User Mode**.
    - b. Enter a password of **novell**; then select **OK**.
    - c. Browse to `/etc/opt/novell/samba`.
    - d. Right-click the `smb.conf` file; then select **Open With > KWrite**.
    - e. Scroll down to the **Share Definitions** section and add the following:

```
[ProjectFiles]
path = /var/ProjectFiles
writable = yes
public = no
group = ACCTUSERS
```

    - f. Select **File > Save**; then select **File > Quit**.

7.  Restart the Samba service by entering:
    - `etc/init.d/novell-smb stop`
    - `etc/init.d/novell-smb start`

8.  Create a Storage Location:
    - a. From iManager under **File Access (NetStorage)**, select **Storage Location: Create**.
    - b. In the Object Name field, enter **ProjectFiles**.
    - c. In the Display name field, enter **ProjectFiles**.
    - d. In the Directory Location field, enter *cifs://10.0.0.x/ProjectFiles*.
    - e. In the Context field, enter *your container*.
    - f. Select **Create**.
    - g. When prompted that the location was created, select **OK**.

9.  Associate the new storage location with the ACCTUSERS group by completing the following:
    - a. Select **Storage Location: Create / Modify List**.
    - b. In the Object field, browse to and select **ACCTUSERS**, *your container*.
    - c. Select **OK**.
    - d. In the Storage Location Objects field, browse to and select *ProjectFiles, your container*; then select **OK**.
    - e. When prompted that the assignment succeeded, select **OK**.
