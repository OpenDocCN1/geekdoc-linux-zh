The Query tab, shown in Figure 10-12, displays the criteria for the modeling query. This information can be helpful when comparing multiple modeling scenarios during the planning phase of your group policy structure.

![](bbox=[0.05, 0.13, 0.82, 0.46])

# CREATING A GROUP POLICY RESULTS QUERY

The Group Policy Results feature in Group Policy Management is equivalent to the Logging mode within the Resultant Set of Policy MMC snap-in. Rather than simulating policy effects like the Group Policy Modeling Wizard, Group Policy Results obtains RSOP information from the client computer to show the actual effects that policies have on the client computer and user environment.

# CREATE A GROUP POLICY RESULTS QUERY

**GET READY.** To view Group Policy Results information, complete the following steps.

+   1.  From the Administrative Tools folder on the Start Menu, open **Group Policy Management** and browse to the forest or domain from which you want to view query results.
+   2.  In Group Policy Management, navigate to and right-click **Group Policy Results**. Select **Group Policy Results Wizard**. On the Welcome to Group Policy Results Wizard page, click **Next**.
+   3.  On the Computer Selection page, select the current computer or click **Browse** to select another computer. Click **Next** to continue.
+   4.  On the User Selection page, select the current user or specify another user for which you wish to obtain policy results and click **Next**.
+   5.  On the Summary of Selections page, verify your criteria and click **Next**.
+   6.  Click **Finish** to close the Completing the Group Policy Results Wizard page.

**STOP. CLOSE** the Group Policy Management console before continuing. View and close the report. Close all open windows.

Like the Group Policy Modeling Wizard, the generated report based on the Group Policy Results criteria includes three tabs. Similar to the Group Policy Modeling Wizard, the Summary tab gives an overall summary of the applied policy settings. The Settings tab provides comprehensive information that includes individual policy settings areas and their resulting effects. Also like the Group Policy Modeling Wizard, clicking the Show All link in the top right corner of the display expands the report's contents. This report can be printed or saved by right-clicking in the display window area and selecting the desired action.