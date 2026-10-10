![](bbox=[0.14, 0.08, 0.6, 0.38])

**Figure 2.21**  Access Control screen from the VShell server.

# SFTP Section

Highlight the SFTP section next (see Figure 2.22). The SFTP section describes the secure file transfer options, which are listed in Table 2.37. These options are also excellent because they allow the control of specific folders to publish to SFTP users. This can help secure a file server by allowing only authorized directories on a file server, such as d:\Common files\, while restricting the users from sensitive operation system files and folders, such as c:\winnt\. This option allows an SSH server to provide full file-system security over an SFTP session without any worries that the user may be able to access and download other files that may be on the SSH server.

**Table 2.37**  Options in the SFTP Section (VShell)

| OPTION | DESCRIPTION |
| :--- | :--- |
| SFTP Root | Sets the SFTP root directory to allow users to access |
| SFTP Root <Directory> that has been specified | Shows the permissions of the SFTP root directory |