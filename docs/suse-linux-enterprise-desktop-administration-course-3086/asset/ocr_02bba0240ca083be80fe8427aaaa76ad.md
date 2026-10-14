+   4. Select **Print via CUPS Network Server**; then select **Next**.
+   5. Select **Remote IPP Queue**; then select **Next**.
+   6. Next to the **Hostname of Print Server** field, select **Lookup**; then select **Scan for IPP Servers**.
+   7. From the drop-down list, select **da1.digitalairlines.com**.
+      - *(Conditional)* If da1.digitalairlines.com does not appear in the drop-down list, enter da1.digitalairlines.com in the field.
+   8. Next to the **Remote Queue Name** field, select **Lookup** to select the default queue configured on da1.
+   9. Test connectivity to the printer server by selecting **Test Remote IPP Access**.
+   10. When a success message appears, select **OK**.
+   11. Select **Next**.
+       - A Queue Name dialog appears.
+       - Notice that **Do Local Filtering** is not selected because filtering is being done on the remote CUPS printer server.
+   12. From the **Name for Printing** field, record the name of the printer queue on the instructor’s server.
+   13. Accept the default settings by selecting **Next**.
+   14. Save the configuration changes by selecting **Finish**.
+   15. Close all windows.

# Objective 3—Understand Novell iPrint

Novell iPrint extends print services securely across multiple networks and operating systems. To use Novell iPrint effectively on SUSE Linux Enterprise Desktop 10, you need to understand the following:

+   - Describe the Purpose and Architecture of Novell iPrint
+   - Configure Novell iPrint
+   - Install the Novell iPrint client

# Describe the Purpose and Architecture of Novell iPrint

To describe the purpose and architecture of Novell iPrint, you need to know the following:

+   - What Novell iPrint Is
+   - Novell iPrint Components on Linux
+   - Novell iPrint Port Usage

**What Novell iPrint Is**  Novell iPrint lets mobile employees, business partners, and customers access printers from a variety of remote locations using existing Internet connections.

![](bbox=[0.941, 0.616, 0.988, 0.662])