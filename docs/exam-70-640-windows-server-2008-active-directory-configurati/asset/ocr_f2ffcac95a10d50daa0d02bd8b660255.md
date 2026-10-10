RSop uses information that is part of the Common Information Management Object Model (CIMOM) database. The CIMOM database is used through WMI and contains information that is gathered when a computer starts and becomes part of the network. This information includes hardware, Group Policy Software Installation Settings, Internet Explorer Maintenance settings, scripts, Folder Redirection settings, and Security settings. When RSop is started in Planning or Logging mode, information in the CIMOM database is used to assist in producing the desired reports.

# USE THE RESULTANT SET OF POLICY WIZARD

GET READY. This exercise will create an RSop Planning mode report, and then create an RSop Logging mode report.

+   1. Click Start, click Run, key mmc, and press(Enter). From the File menu, select Add/Remove Snap-in, and then click the Add button.

+   2. Select the Resultant Set of Policy snap-in from the Add Standalone Snap-in window, click Add, and then click Close.

+   3. Click OK to finish creating the new console window.

+   4. In the left console pane, select Resultant Set of Policy.

+   5. From the Action menu, select Generate RSop Data to launch the RSop Wizard. Click Next.

+   6. In the Mode selection page, select Planning Mode and click Next to continue.

+   7. In the User and Computer Selection page, complete the appropriate fields to select the user or computer for which you wish to simulate policy settings. Click Next to proceed.

+   8. In the Advanced Simulation Options page, you can choose to simulate your policy with additional conditions, such as slow links and loopback processing. The settings in this window are optional. The loopback processing option is only available if you chose to simulate settings for a user and computer. Click Next to continue.

+   9. On the User Security Groups page, you can choose to simulate the effect of changing the user's security group memberships. The settings on this page are optional. Click Next to continue.

+   10. On the Computer Security Groups page, you can simulate changes to the computer's security groups. The settings on this page are optional. Click Next to continue.

+   11. On the WMI Filters for Users page, select any filters that you would like to include in your simulation. The page settings here are optional. Click Next to continue.

+   12. On the WMI Filters for Computers page, select any filters that you would like to include in your simulation. The page settings here are optional. Click Next to continue.

+   13. On the Summary Of Selections page, review your simulation query information, change the domain controller on which you wish to process the simulation if necessary, and click Next to generate the report.

+   14. Click Finish to close the wizard. The results of your query will be displayed in an MMC window that looks similar to a Group Policy Object Editor window. The MMC can be saved with the results of the query.

+   15. In the left console pane, select Resultant Set of Policy.

+   16. From the Action menu, select Generate RSop Data to launch the RSop Wizard. Click Next.

+   17. From the Mode Selection page, select Logging Mode and click Next to continue.