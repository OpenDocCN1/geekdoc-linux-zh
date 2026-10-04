
# Acquire permission settings?

| Permission | Roles | | | | | |
| --- | --- | --- | --- | --- | --- | --- |
| Acquire permission settings? | Anonymous | Friends | Manager | Owner | | |
| Access contents information | | | | | | |
| Add Accelerated HTTP Cache Managers | | | | | | |
| Add Database Methods | | | | | | |
| Add Documents, Images, and Files | | | | | | |
| Add External Methods | | | | | | |
| Add Folders | | | | | | |
| Add MailHost objects | | | | | | |
| Add Python Scripts | | | | | | |
| Add RAM Cache Managers | | | | | | |

Figure 6-2: Activated "Acquire permission settings?" checkboxes

## 6.1.4.1 Acquire permission settings?

The right-hand columns in the permissions list define the roles for the current folder. When the Acquire permissions checkbox is checked (the default, shown in 6.2), acquisition is active for the relevant permission, and the current folder acquires its permission and role settings from the next highest folder.

If Acquire permission settings? is active in that next highest folder, that folder acquires the settings from the one above it and so on, up the hierarchy to the root folder. The permissions set for a folder (or folderish object) can spread quite far, depending on how extensively the setting Acquire permission settings is activated in the object hierarchy.

Acquisition is more complicated than this, however. if you look at the roles in the Security screen (Figure 6-3), you see checkboxes beneath them as well. These checkboxes allow Zone to manage permissions among roles differently from their subordinate managers.

![](img/43a28cce5475b2f487bf455365567fb6_132_0.png)

Figure 6-3: Security screen for an activated folder

Users, Roles, and Security 115

For example, imagine that we have a hierarchy consisting of a State folder, containing a County folder, which in turn contains a City folder (Figure 6-4) We see the permission Access contents information in the Security tab of all three folders. If Acquire permission settings? activated for this permission in both County and City (as it is by default), then all roles in City will acquire their settings for Access contents information from the County and State folder and above State up to the Root folder via acquisition. Changes to the permission made in State will also affect County and City. Changes made to County will affect City (but not State), and changes made to City will only affect it.

![](img/43a28cce5475b2f487bf455365567fb6_133_0.png)

Figure 6-4: Example folder hierarchy

Acquiring permissions works well, assuming you want the subordinate folders to have permissions granted in their parents; but what if you want the Access contents information permission granted to a particular role in State, but not to County contained in it?

In County, first deactivate Acquire permission settings? for the Access contents information permission and make sure that the opposite Access contents information under the role you are restricting is deactivated. Deactivating Acquire permission settings? means that none of the roles in County will inherit this permission setting from State—so you may need to manually activate the checkboxes for other roles to which you still want to grant this permission.

If, however, you want to reactivate the permission for the City folder contained by County, you will no longer be able to use acquisition because the permission is not set for the role in the County folder. Instead, you would need to set the permission explicitly in City using the checkbox under the role to the right of the Access contents information permission.

We see here that deactivating the Acquire permission settings? for Folder X in a hierarchy breaks the acquisition chain for this permission. If you then activate Acquire permission settings? for this permission in a subfolder of Folder X, a new acquisition chain begins from that subfolder and continues through successive layers of folders thereafter.

NOTE: The example given above also applies to non-folderish objects—which are always at the end of the acquisition chain because they cannot contain additional subobjects.

By combining acquisition (use Acquire permission settings?) with directly activating oractivating roles, you can modify permissions to meet your security requirements. (This will be illustrated in 8.3, "Example: Authentication," with a simple but important example of authentication).

Because acquisition can make it difficult to see exactly which permissions are granted to a given object, it can sometimes be beneficial to deactivate Acquire permission settings? for all permissions and set them all explicitly. This is especially true of objects that must be tightly secured because they have the potential to be destructive or expose sensitive data.

Acquisition makes it easier and more efficient for Zone programmers and administrators to create and make websites. For example, using the Zone programmer to create all necessary roles in the root folder and set the permissions according to their defaults. Once these changes are saved, the settings apply to all folders and subfolders in well as all folders that you later create. To set different permissions for one or more objects, we simply deactivate the appropriate Acquire permission settings checkbox for the relevant object and change the permissions as required. (Remember that in doing so you are breaking the security acquisition chain.) All subobjects default to the same permissions as the object where the acquisition chain was broken (if the Acquire permission settings? checkbox is still activated for the subobjects).

Because administrators cannot always know when roles are added or changed through the hierarchy, you should devote adequate time to designing the security structure in large projects. Carefully consider which permissions are required and how many different user roles there should be.

## 6.1.5 Ownership

The user who creates a new object in Zone automatically becomes object's owner, granting them the permissions assigned to the owner role on that object. The Ownership tab on an object is used to inspect and modify the current ownership of an object.

When you click on the Ownership tab (shown in Figure 6-5), you open the Ownership screen for the object (Figure 6-6). The Ownership screen shows who owns the object—that is, the object's creator. Objects created during the Zone installation are unowned.

| Contents | View | Properties | Security | Undo | Ownership | Find |
| --- | --- | --- | --- | --- | --- | --- |

Figure 6-5: The Ownership tab

All Doc objects can be owned. When you create an object, you decide its owner. Ownership matters for methods; it determines what they do when they are executed. See the 'Properties' view of method objects for more information.

This object is unowned

Figure 6-6 Ownership screen of the root folder (unowned)

### 6.1.5.1 Ownership When Importing

When you import objects (Figure 6-7), you can retain your current ownership settings or become the new owner (for more information on importing, see section 3.1.9.3, 'Importing Objects').

![](img/43a28cce5475b2f487bf455365567fb6_135_0.png)

Import file name

| Ownership | Take ownership of imported objects, Retain existing ownership information | Import |
| --- | --- | --- |

Figure 6-7: Importing an object

The Ownership screen shows the user who owns the object. Users who do not own the objects see only the text indicating who does own the objects (although users with permission to Take Ownership see the Take Ownership button (shown in Figure 6-8). If you click the Take Ownership button, you become the owner of the object.

![](img/43a28cce5475b2f487bf455365567fb6_135_1.png)

All Doc objects can be owned. When you create an object, you decide its owner. Ownership matters for methods; it determines what they do when they are executed. See the 'Properties' view of method objects for more information.

This object is owned by manager (ad_users).

If you take Take Ownership, you will take ownership of an object; usually when doing so you could also take ownership of sub-objects as well.

![](img/43a28cce5475b2f487bf455365567fb6_135_2.png)

Figure 6-8: Ownership screen with Take Ownership button
