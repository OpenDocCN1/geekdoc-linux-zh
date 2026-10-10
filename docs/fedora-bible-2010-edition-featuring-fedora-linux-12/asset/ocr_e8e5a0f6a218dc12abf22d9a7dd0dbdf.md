+   • **See more information** — Double-click the entry to see an address book card with as much information as is available for the person displayed.
+   
+   • **Write to an LDAP person** — Click the highlighted e-mail address and select write to open a Compose window, ready to create and send an e-mail to the person selected.
+   
+   • **Add the LDAP server to compose email** — Select Edit → Preferences, choose the Composition button, then choose the address tab. Check the Directory Server. From the drop-down box you can choose the LDAP server you just added to Thunderbird. The next time you compose a message, typing an e-mail address will auto-complete with addresses from your LDAP directory.

![](bbox=[0.17, 0.29, 0.86, 0.65])

Figure 21-2: Search an LDAP address book directory by name, e-mail address, or other information.

If your LDAP directory is not accessible from the Thunderbird client, run the Thunderbird or other LDAP-enabled e-mail application on the LDAP server. If you are able to access the LDAP directory from the local server, it means that for some reason requests are being rejected from the server to outside hosts. Verify that the firewall on the server has port 389 open (which is used by default to access LDAP services). Next, check how access permissions are being set in the slapd.conf file.