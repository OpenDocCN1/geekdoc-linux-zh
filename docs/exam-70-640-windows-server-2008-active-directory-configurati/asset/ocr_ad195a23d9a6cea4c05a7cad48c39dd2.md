+   • **Delegation.** The Delegation tab, shown in Figure 10-4, displays groups and users with permission to link, perform modeling analyses, or read group policy results information. Modeling is the same as planning mode using RsOP. Reading results data is the same as RsOP’s logging mode. Also located on this tab is an Advanced button that allows administrators to access the Group Policy Object’s Security tab.

![](bbox=[0.05, 0.16, 0.2, 0.22])

![](bbox=[0.25, 0.17, 0.85, 0.4])

# Managing an Individual GPO

> As illustrated previously, Group Policy Management allows administrators to create and modify policies from the container on which they are linked. Additionally, all aspects of each individual policy, including the scope of its application, filtering methods, enabled or disabled status, effective settings, and delegation of application and management, can be managed using Group Policy Management. The tabbed display interface is organized logically, easy to navigate, and simplifies modifications.

The following list explains and illustrates the features available on each tab when a GPO is selected in the Group Policy Management interface:

+   • **Scope.** As shown in Figure 10-5, this tab allows administrators to view the locations to which the policy is linked. In addition, security filtering using permissions and WMI are available for viewing, editing, or creating. When a WMI filter is applied to the policy, it appears in the list with an Open button that allows filter modification. If a WMI filter is not applied to the policy, the Open button will allow a new filter to be created or linked to the GPO.

+   • **Details.** This tab, shown in Figure 10-6, allows the GPO to be enabled or disabled. It also displays read-only information that includes the owner, GUID, creation date, and last modification date.

+   • **Settings.** When this tab is activated, an HTML report is generated that allows administrators to view GPO settings that do not have the original default values. Links on the right side of the report allow detailed information to be displayed or hidden. Right-clicking within this view allows administrators to print or save the report.

+   • **Delegation.** Like the previously discussed Delegation tab for a container object, this tab lists the users and groups that have access to this GPO and the permissions that apply to them. The Advanced button allows access to the Security tab to directly view the GPO’s ACL.

Now that you have a clearer picture of the Group Policy Management tool and its interface, we will discuss several policy management techniques and how to accomplish them using this tool.