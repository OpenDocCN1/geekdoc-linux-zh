+   c. Preventing the usb_storage kernel module from loading at system initialization
+    d. Physically removing or restricting access to CD-ROM drives, DVD-ROM drives, and USB ports

# Discovery Exercises

![](bbox=[0.06, 0.3, 0.22, 0.42])

# Creating a Lockdown Security Profile

Security planning is vital when planning to lock down computers within your organization. Effective security planning ensures that security loopholes are detected in a flawed design before they are implemented.

You are about to implement several new publicly accessible kiosks for individuals who want to browse your company catalog. This catalog is made available on the Internet and will be accessed using Firefox from the kiosks. Kiosk users should be restricted to using the Firefox application only and should not have any access to other areas of the desktop or removable media. In addition, they should not be able to customize Firefox or change its default home page. The administrator user account should have full access to the system to perform system maintenance.

Write a short summary of the steps needed to perform this lockdown. Include the names of the technologies and tools involved and how they can be used to lock down the kiosks. If there are multiple methods that can be used to lock down a particular area, provide a rationale for the method you chose.

# Locking Down Computers

Assume that your PC is a publicly accessed kiosk and configure GConf to lock it down using the summary you created in the previous Discovery Exercise. Test your results to ensure that the lockdown is effective.

# Researching Lockdown Utilities

Locking down Linux computers has been a standard practice for over a decade. As a result, there are many software packages in addition to GConf that can be used to restrict access to various Linux components or lock down the entire Linux desktop. Use the Internet to research three lockdown packages. For each, describe their function and basic configuration. Next, compare each lockdown package to GConf. Summarize your findings in a brief memo.