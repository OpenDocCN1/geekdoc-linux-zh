existing branches. Furthermore, the more branches that ACME opens up, the more pro-  
hibitive it becomes to connect them to the existing locations via dedicated leased lines.  
Virtual private networking capitalizes on the ubiquity of the Internet to offer a cost-  
effective, distance-insensitive alternative to private WAN links. There are two steps to  
building a VPN:

+   - Connect all branches to the Internet by purchasing a connection to an ISP with a  
+     *local point of presence* (POP), also known as a *hub*.
+   - Once all branches can reach each other via the Internet, build *virtual* links over the  
+     existing Internet IP infrastructure to ensure the confidentiality and integrity of the  
+     data as it travels from branch to branch.

Figure 12.2 shows the ACME WAN network using a VPN design.

# **Figure 12.2** ACME’s VPN connections

![](bbox=[0.11, 0.43, 0.9, 0.78])

The advantages of VPNs over dedicated leased lines are three-fold:

**Distance-Independent Connection Costs** The fact that each new corporate branch  
can connect to the other branches using an Internet connection, regardless of the  
location of the rest of the branches, reduces cost. The cost of the local loop is kept  
to a minimum and is often bundled into the monthly charges from the ISP. In addi-  
tion, some ISPs offer discounts with quantity connection orders and now all of the  
offices have Internet access also, but this would not be a benefit in some cases.