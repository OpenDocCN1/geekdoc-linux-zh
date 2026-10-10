+   * **5.** Select the scope of replication for this zone from the following options and click **Next** to continue:
+   	* All DNS servers in the Active Directory forest
+   	* All DNS servers in the Active Directory domain (this is the default value)
+   	* All domain controllers in the Active Directory domain (for backward compatibility with Windows 2000)
+   	* To all domain controllers specified in the scope of a manually created application partition
+   * **6.** Select the option to create an IPv4 reverse lookup zone if your network uses TCP/IP version 4 as its network protocol, or select the option to create an IPv6 reverse lookup zone if you have upgraded your networking hardware to use the new TCP/IP version 6. Click **Next** to continue.
+   * **7.** In the Reverse Lookup Zone Name dialog box, click the **Network ID** option and enter the Network ID of the reverse lookup zone. The Reverse Lookup zone name should appear in the second option field. Click **Next** to continue.
+   * **8.** Select the level of secure updates that should be enabled for this zone from the following options and click **Next:**
+   	* Allow only secure dynamic updates—this is the default option.
+   	* Allow both nonsecure and secure dynamic updates.
+   	* Do not allow dynamic updates.
+   * **9.** Review the summary zone creation window and click **Finish** to complete the process.
+   * **10.** If you haven't enabled dynamic updates, add any necessary resource records by right-clicking on the newly created zone and selecting **New Pointer (New PTR)**. For example, you should create a PTR record that references any server A records that you have created in forward lookup zones on the server.

**PAUSE.** Reverse lookup zones were created.

Reverse lookup zones are not required or configured by default. However, it is good practice to add reverse lookup zones for troubleshooting, security checks, and reverse IP queries. A reverse lookup zone is called an in-addr.arpa domain and uses the reverse dotted decimal notation of a forward lookup zone. For example, if the forward lookup zone uses 192.168.1.200 for its IP address, the reverse lookup zone would appear as 200.1.168.192- in-addr.arpa. In addition to the zone creation, a resource record called a *pointer (PTR)* record is necessary to map the address back to a host in the corresponding forward lookup zone.

# Raising the Domain and Forest Functional Levels

> To leverage more advanced features in Active Directory, you can raise the domain and forest functional levels within Active Directory after you have retired any domain controllers that are running down-level operating systems, such as Windows 2000. Lesson 1 mapped out the differences between each level in terms of supported operating systems and functionality. In this lesson, the focus is on the how-to steps and requirements for raising the functionality level.

Domain and forest functional levels are available to provide backward compatibility with previous Windows Server operating systems. Migrating your network to one consistent platform provides many administrative benefits and can lower the overall network cost of ownership. Prior to raising the domain functional levels, verify that any previous Microsoft Windows network operating systems are not needed in the domain. Careful planning will be required for each company and their current network structure. If an organization is interested in any future acquisitions or mergers, raising the domain level could have an impact, and this should be taken into careful consideration. For example, if an enterprise organization