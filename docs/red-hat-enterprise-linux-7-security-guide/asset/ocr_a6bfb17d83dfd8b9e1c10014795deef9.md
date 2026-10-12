# 7.3.5. Saving SCAP Content

SCAP Workbench also allows you to save SCAP content that is used with your system evaluations. You can either save a customization file separately (see Section 7.3.4, "Customizing Security Profiles") or you can save all security content at once by clicking the Save content combo box and selecting either the Save into a directory or Save as RPM options.

By selecting the Save into a directory option, SCAP Workbench saves both the XCCDF or datastream file and the customization file to the specified location. This can be useful as a backup solution.

By selecting the Save as RPM option, you can instruct SCAP Workbench to create an RPM package containing the XCCDF or data stream file and customization file. This is useful for distributing the security content to systems that cannot be scanned remotely, or just for delivering the content for further processing.

![](bbox=[0.08, 0.3, 0.9, 0.7])

Figure 7.6. Saving the Current SCAP Content as an RPM Package

# 7.3.6. Viewing Scan Results and Generating Scan Reports and Remediations

After the system scan is finished, three new buttons, Clear, Save Results, Generate remediation role, and Show Report will appear instead of the Scan button.