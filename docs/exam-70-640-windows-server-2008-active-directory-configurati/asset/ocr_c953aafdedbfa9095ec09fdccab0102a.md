GPOs are not modified during an import or copy operation. Table 10-1 details the differences between Import and Copy within the Group Policy Management snap-in.

# **Table 10-1**
GPMC Copy Versus Import

| COPY | IMPORT |
| :--- | :--- |
| Source: An existing GPO within Active Directory. | Source: Any GPO that was backed up and stored in the file system. |
| Destination: Creates a new GPO in Active Directory. This new GPO will have a unique GUID. | Destination: Erases the existing settings of an existing GPO in Active Directory. |
| ACL: Can use the default ACL for new GPOs or copy the ACL from the source GPO. | ACL: Not modified in the destination GPO. |
| Required Permissions: The right to create GPOs in the target location and Read access to the source GPO are required. | Required Permissions: Read permission to the source GPO and edit rights to the destination GPO. |

+   * **Backup and restoration of GPOs is available in Group Policy Management.** The Group Policy Management Backup feature allows a GPO to be exported to the file system and stored for disaster recovery or testing. Multiple versions of the same GPO can be backed up to the same file system directory. The Restore feature allows a specific GPO to be restored to a prior state. If multiple settings are modified that produce undesirable results, the Restore feature provides a contingency solution. It restores all attributes, settings, Access Control Lists (ACLs), GUIDs, and links to any Windows Management Instrumentation (WMI) filters.

+   * **Resultant Set of Policy (RSoP) functionality integration includes Group Policy Modeling and Group Policy Results.** RSoP is a query engine that looks at GPOs and then reports its findings. Use this tool to determine the effective settings for a user or a computer based on the combination of the local, site, domain, domain controller, and OU policies. RSoP was originally created as a separate MMC snap-in. The two modes, planning and logging, are renamed in GPMC to Group Policy Modeling and Group Policy Results. We will discuss RSoP in further detail later in this lesson.

+   * **Hypertext Markup Language (HTML) reports allow read-only views of GPO settings and RSoP information.** This information is easily acquired and easy to save or print for documentation or analysis purposes.

+   * **Search for GPOs based on name, permissions, WMI filter, GUID, or policy extensions set in the GPOs.**

+   * **Search for individual settings within a GPO by keyword and search for only those settings that have been configured.**

+   * **GPMC is natively installed with Windows Server 2008.** In previous versions of the operating system, it needed to be manually downloaded from the Microsoft Web site.

In addition to the primary capabilities listed previously and the new management interface, the GPMC provides a simplified method of delegating GPO management. We will discuss GPO delegation and the remaining GPO topics within the context of this new management tool.