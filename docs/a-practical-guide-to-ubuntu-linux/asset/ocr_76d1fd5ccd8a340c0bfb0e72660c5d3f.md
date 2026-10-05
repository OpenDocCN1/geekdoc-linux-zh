# 768 CHAPTER 21 NIS AND LDAP

![](bbox=[0.365, 0.095, 0.735, 0.458])

Figure 21-1 The New Address Book window, General tab

General tab Select On LDAP Servers from the drop-down list labeled Type. Evolution will use to refer to this LDAP directory in the text box labeled Name; the examples use employees. Enter the FDN of the LDAP server in the text box labeled Server. If you are experimenting on the local system, enter localhost in this box. If appropriate, change the value in the text box labeled Port. To follow the example in this chapter, select No encryption from the drop-down list used secure connection.

Details tab Next click the tab labeled Details (Figure 21-2). Find Possible Search Bases. If all is working properly, Evolution will display the Supported Search Windows. Highlight the DN of the directory you want to use and click OK. Evolution displays the selected DN in the text box labeled Search base. Select Sub from the drop-down list Search scope to enable searches at all levels of the directory. Click OK. Next click the Contacts button at the lower-left corner of the Mail-Evolution window. CouchDB, On this Computer, and On LDAP servers at the left side of the window. If the name of the address book you specified (employees in the example) does not appear below On LDAP servers, click the plus (+) to the left of this label. Then click the name of the address book you want to work with. Evolution prompts for the LDAP administrator password. Enter the