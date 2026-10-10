
RSop uses information that is part of the Common Information Management Object Model (CIMOM) database. The CIMOM database is used through WMI and contains information that is gathered when a computer starts and becomes part of the network. This information includes hardware, Group Policy Software Installation Settings, Internet Explorer Maintenance settings, scripts, Folder Redirection settings, and Security settings. When RSop is started in Planning or Logging mode, information in the CIMOM database is used to assist in producing the desired reports.

# USE THE RESULTANT SET OF POLICY WIZARD

GET READY. This exercise will create an RSop Planning mode report, and then create an RSop Logging mode report.

- 1. Click Start, click Run, key mmc, and press (Enter). From the File menu, select Add/Remove Snap-in, and then click the Add button.
- 2. Select the Resultant Set of Policy snap-in from the Add Standalone Snap-in window, click Add, and then click Close.
- 3. Click OK to finish creating the new console window.
- 4. In the left console pane, select Resultant Set of Policy.
- 5. From the Action menu, select Generate RSop Data to launch the RSop Wizard. Click Next.
- 6. In the Mode selection page, select Planning Mode and click Next to continue.
- 7. In the User and Computer Selection page, complete the appropriate fields to select the user or computer for which you wish to simulate policy settings. Click Next to proceed.
- 8. In the Advanced Simulation Options page, you can choose to simulate your policy with additional conditions, such as slow links and loopback processing. The settings in this window are optional. The loopback processing option is only available if you chose to simulate settings for a user and computer. Click Next to continue.
- 9. On the User Security Groups page, you can choose to simulate the effect of changing the user's security group memberships. The settings on this page are optional. Click Next to continue.
- 10. On the Computer Security Groups page, you can simulate changes to the computer's security groups. The settings on this page are optional. Click Next to continue.
- 11. On the WMI Filters for Users page, select any filters that you would like to include in your simulation. The page settings here are optional. Click Next to continue.
- 12. On the WMI Filters for Computers page, select any filters that you would like to include in your simulation. The page settings here are optional. Click Next to continue.
- 13. On the Summary Of Selections page, review your simulation query information, change the domain controller on which you wish to process the simulation if necessary, and click Next to generate the report.
- 14. Click Finish to close the wizard. The results of your query will be displayed in an MMC window that looks similar to a Group Policy Object Editor window. The MMC can be saved with the results of the query.
- 15. In the left console pane, select Resultant Set of Policy.
- 16. From the Action menu, select Generate RSop Data to launch the RSop Wizard. Click Next.
- 17. From the Mode Selection page, select Logging Mode and click Next to continue.
- 18. On the Computer Selection page, you can select This Computer or select Another Computer and key the name of the computer. If you are not sure of the computer name, you can click Browse to find the computer for which you wish to perform the query. The other option on this page is to click the Do Not Display Policy Settings for the Selected Computer in the Results Display checkbox. This will eliminate the computer policy settings from the results window. Click Next to continue.
- 19. On the User Selection page, select the appropriate bullet for the user for which you wish to display query results. If you chose a computer in step 7 and do not wish to have user policy settings displayed in the final results, you can click the Do Not Display User Policy Settings in the Results checkbox. Click Next to continue.
- 20. On the Summary of Selections page, verify your desired query information, click the checkbox to show error information, and click Next to begin the analysis. Click Finish to close the wizard. The MMC window will display the results of your request.

PAUSE. CLOSE the MMC console before continuing.

To create an RsOP query for an existing computer or user, you must be logged on to the local computer as a user, be a member of the local Administrators, Domain Administrators, or Enterprise Administrator group, or have permission to generate an RsOP for the domain or OU in which the user and computer accounts are contained. If the RsOP query includes site GPOs that cross domain boundaries in the same forest, you must be logged on as an Enterprise Administrator. The results that are displayed for the RsOP query look very similar to the information available when editing or creating a GPO using the Group Policy Object Editor. However, only the settings that have been altered from the default will be displayed. Changes to a policy will not be reflected unless the RsOP query is run again after a GPO has been refreshed by a computer restart, user logon, or the use of gpupdate.exe.

## Creating a Group Policy Modeling Query

The same information that is gathered and reported using the Resultant Set of Policy snap-in can be gathered and reported using the Group Policy Management utility. In fact, it is even simpler to use the Group Policy Management utility to obtain information than to use the Resultant Set of Policy snap-in. Individual settings that affect the user are easy to find, and multiple queries can be created and stored within one interface. To view query results using the Resultant Set of Policy MMC snap-in, it is necessary to save each individual console window. You must run multiple instances of the Resultant Set of Policy MMC snap-in to compare results. In contrast, using the Group Policy Management tool permits multiple queries available within the same interface for comparison purposes. In addition, the interface allows administrators to save the reports for future reference and print them directly from the HTML window pane.

This section will demonstrate how to use the Group Policy Modeling and Group Policy Results features of Group Policy Management to obtain RsOP information. **Group Policy Modeling**, referred to as *Planning mode* using the Resultant Set of Policy snap-in, is used to simulate the effect of a policy on the user environment.

# CREATE A GROUP POLICY MODELING QUERY

GET READY. To create a query, complete the following steps using Group Policy Management.

- 1. From the **Administrative Tools** folder on the Start menu, open **Group Policy Management** and browse to the forest or domain in which you want to create a Group Policy Modeling query.
- 2. Right-click **Group Policy Modeling** and then click **Group Policy Modeling Wizard**.
- 3. On the Welcome to the Group Policy Modeling Wizard page, click **Next**.
- 4. Complete the remaining pages, entering the information that will build the appropriate simulation criteria. These remaining pages are the same as those you completed using the Resultant Set of Policy MMC in Planning mode.

PAUSE. View the generated report.

The generated report contains three tabs to organize and display important information about the query. The Summary tab in the newly created Group Policy Modeling query report will show a summary of information collected during the simulation process. Figure 10-11 shows an example of a Summary report.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_256_0.png)

The Settings tab provides comprehensive information that includes individual policy settings areas and the effects each would have in a live deployment. Click the *show all* link in the top right corner of the display to expand the report's contents. This report can be printed or saved by right-clicking in the display window area and selecting the desired choice.
