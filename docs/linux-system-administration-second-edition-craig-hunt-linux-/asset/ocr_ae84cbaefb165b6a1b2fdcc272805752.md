![](bbox=[0.17, 0.04, 0.85, 0.56])

Figure 11.7: The New Account dialog box allows you to enter critical information provided by your ISP.

+   4. Enter a name in the Connection Name field. You can use any name you like; this entry is used to help you identify an account if you have several.

+   5. Click **Add** to add a telephone number. KPPP displays a small dialog box in which you enter a telephone number.

+   6. In the New Account dialog box, select the authentication method your ISP uses. In most cases, you may leave this set to its default of PAP.

+   7. Click through the remaining tabs on the New Account dialog box and enter any information provided by your ISP. The information that’s most likely to need setting is the DNS server information. Select the **Manual** option, enter an IP address in the **DNS IP Address** field, and click **Add**. Repeat this process if your ISP provides two DNS server addresses. In some cases, you may need to create a login script, similar to the one described for script-based PPP dialups. It’s often not necessary to configure a DNS address, because this information may be transferred as part of the PPP negotiation.

+   8. Click **OK** in the New Account dialog box.

+   9. In the **Configuration** window, click the **Device** tab. Check that the **Modem Device** is set appropriately, and set the **Connection Speed** to 115,200. (You may want to use a lower speed if your modem is particularly slow. In general, you should use a connect speed of at least twice the modem’s official speed, because modems support compression technologies that increase their effective speed when handling uncompressed data.)