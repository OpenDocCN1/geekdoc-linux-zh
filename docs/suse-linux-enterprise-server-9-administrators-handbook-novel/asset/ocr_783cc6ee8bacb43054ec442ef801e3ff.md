+   - **Scan Options—**On this tab, you can select the number of hosts and tests to run simultaneously. This tab also allows you to select which options are used for port discovery on the target.
+   - **Target—**You can specify a name or address for the target system on this tab. The software also supports defining multiple targets and retrieving a target list from a disk file.
+   - **User—**User-customized rules can be included using this selection.
+   - **Prefs.—**This tab permits fine-tuning the various aspects of the port scanning options. This is also the place where the SNMP community string used for scanning can be changed from public to a more appropriate value. Using this tab, you can also define accounts to be used for insecure services such as FTP, POP, and HTTP.

**FIGURE 12.1**  
The Nessus Client login screen.

![](bbox=[0.283, 0.446, 0.67, 0.723])

Upon successful login, you are presented with the Plugins tab as well as a warning message (see Figure 12.2). A number of known exploits are Denial of Service exploits (DoS) that cause services to fail. To properly measure the exposure of a system, you must test for the vulnerability using the same approach as the attack. If the system is vulnerable, the service will fail, causing an outage. By default, Nessus disables these tests.

A more detailed version of the Plugins tab is shown in Figure 12.3. In the upper portion of the tab is a list of the different families of tests. If you want to