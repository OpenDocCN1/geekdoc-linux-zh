the example uses **employees**. Enter the FQDN of the LDAP server in the text box labeled **Server**. If you are experimenting on the local system, enter **localhost** in this box. If appropriate, change the value in the text box labeled **Port**. To follow the example in this chapter, select **No encryption** from the drop-down list labeled **Use secure connection**.

In the section labeled **Authentication**, select **Using distinguished name (DN)** from the drop-down list labeled **Login method**. Enter the DN of the LDAP administrator in the text box labeled **Login** (the example uses **cn=ldapadmin,dc=soxell,dc=com**).

![](bbox=[0.18, 0.3, 0.27, 0.33])

Next click the tab labeled **Details** (Figure 21-2). Click **Find Possible Search Bases**. If all is working properly, Evolution will display the Supported Search Bases window. Highlight the DN of the directory you want to use and click **OK**. Evolution displays the selected DN in the text box labeled **Search base**. Select **Sub** from the drop-down list labeled **Search scope** to enable searches at all levels of the directory. Click **OK**.

Next click the **Contacts** button at the lower-left corner of the Mail-Evolution window. **On this computer** and **On LDAP** servers appear at the left side of the window. If the name of the address book you specified (**employees** in the example) does not appear below **On LDAP** servers, click the triangle to the left of this label. Then click the name of the address book you want to work with. Evolution prompts for the LDAP administrator password. Enter the password and click **OK**. Evolution highlights the name of the address book; you can now search the LDAP database.

Enter the name of an entry in the Search text box at the upper-right corner of the window and press **RETURN**. Evolution displays the entry. Figure 21-3 on the next page shows the result of following the example in this chapter and entering **Mark** in the Search text box.

![](bbox=[0.35, 0.64, 0.85, 0.88])

**Figure 21-2** The New Address Book window, Details tab