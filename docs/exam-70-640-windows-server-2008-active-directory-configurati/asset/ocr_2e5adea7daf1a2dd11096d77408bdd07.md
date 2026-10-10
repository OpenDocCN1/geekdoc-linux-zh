+   4. If you chose Basic-Redirect Everyone's Folder To The Same Location, you must specify the Target folder location in the Settings dialog box. Choose from the following options:

+   - Create A Folder For Each User Under The Root Path. This option is the default. When a user's folders are redirected using this setting, a subfolder is automatically created using the username based on the %username% variable and the folder name of the redirected folder. Allowing the system to create the subfolder structure automatically ensures that the appropriate user permissions are implemented. However, for the subfolder structure creation to work, each user must have appropriate permissions on the shared folder to create a folder. For the root path, use a Universal Naming Convention (UNC) name, rather than a drive letter-referenced path, which may change.

+   - Redirect To The Following Location. This option allows you to specify the path used to redirect the Documents folder. Use this option to redirect the folder to a server share or to another valid local path. When specifying a path, use a UNC name, rather than a drive letter-referenced path, which may change.

+   - Redirect To The User's Home Directory. This option redirects the Documents folder to a preconfigured home directory for the user. This setting is not recommended unless you have already deployed home directories in your organization and wish to maintain them. Security is not checked automatically using this option, and the assumption is made that the administrator has placed appropriate permissions on the folders. Administrators have full control over the users' My Documents folders when they are redirected to the user's home directory, even if the Grant The User Exclusive Rights To Documents checkbox is selected.

+   - Redirect To The Local User Profile Location. This option allows administrators to return redirected folders to their original default locations. This setting copies the contents of the redirected folder back to the user profile location. The redirected folder contents are not deleted. The user continues to have access to the content of the redirected folder, but access is provided from the local computer, instead of the redirected location.

+   5. If you chose Advanced-Specify Locations For Various User Groups in step 3, you must specify the target folder location for each group that you add in the Settings dialog box. The choices are the same as those outlined in step 4; however, you need to associate each group selected with a specific target location. Click Add to select the groups and choose the target folder location for redirected files.

+   6. The Settings tab of the Documents Properties dialog box provides several additional selections. Select the Grant The User Exclusive Rights To Documents and Move The Contents Of Documents To The New Location checkboxes, if necessary. If you will be supporting down-level clients running Windows 2000, Windows XP, or Windows Server 2003, place a checkmark next to Also apply redirection policy to Windows 2000, Windows 2000 Server, Windows XP, and Windows Server 2003 operating systems.

+   7. Select from the following options in the Policy Removal box of the Settings tab:

+   - Leave The Folder In The New Location When Policy Is Removed. This option keeps the redirected folder in its redirected location, without doing anything to the data. If the policy is removed, the user continues to have access to the contents at the redirected folder.

+   - Redirect The Folder Back To The Local Userprofile Location When Policy Is Removed. With this option enabled, the folder and its contents are copied back to their user profile location. The user can continue to access the contents on the local computer. With this option disabled, the folder returns to its user profile location, but the contents are not copied or moved back with the redirection process. The user can no longer see or access the files.

+   8. Click OK.

PAUSE. CLOSE the Group Policy Management Editor window.