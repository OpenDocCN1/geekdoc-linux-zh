+   6. configure the firewall's basic rules and logging:
+   
+   – enable detailed logging. (When the firewall is up and running OK you may want to decrease the verbosity of the logs.)
+   
+   – set the firewall to block everything, in and out
+   
+   7. insert the firewall into your network
+   
+   8. modify any settings on LAN machines that have to take account of the firewall. For example, if you've just enabled NAT, you'll have to renumber your LAN PCs. The default gateway for the LAN PCs depends on your configuration and firewall type, so you'll have to check your documentation. If you're using NAT, the default gateway is usually the firewall's internal interface address. (This without NAT, it could be either the firewall's internal interface, or the firewall's own default gateway. (See under “Proxy ARP” in the Notes for why there are two different possibilities.)
+   
+   9. refine your firewall rules:
+   
+   – on paper, translate your security policy into a set of firewall rules
+   
+   – apply these rules to the firewall.

We've usually found it's best to apply rules in stages. First allow outgoing **ping** traffic, and check that that part works correctly. Then allow other outgoing traffic, and check it, before allowing traffic initiated from outside. (This implicitly assumes that you're using an SPI firewall.) Finally, if you have a DMZ, configure it and apply any necessary rules.

We use a checklist to remind us of what tests we need to do, and to record the results (Appendix 25).

You will probably need to check that certain TCP services (e.g. HTTP, SMTP) are accessible from outside, but it's unlikely you have the necessary servers on your test “inside” PC. You can either enable the **daytime** service and modify your rules accordingly for testing, or alternatively run `netcat` on the inside machine – acting as a “manual” server listening on the appropriate port, as we described in Modules 17.5 and 17.4

+   10. when the firewall is behaving as you want it:
+   
+   • save its configuration settings to file, and store them on a safe machine on your LAN, *not on the firewall*. In the same location, save the firewall software (or firmware if it's an appliance). See Web Appendix 3X for the convention we use to make sure we have everything we need to restore our firewall configs
+   
+   • continue with your network implementation as described in Chapter 23.

# Adding a firewall to an existing live network

If you're adding the firewall into an existing live network, it's often easiest if you build a small test network first, so you can familiarize yourself with the firewall without disrupting anyone else. Add one machine “outside” the firewall and one machine “inside,” to simulate the WAN and LAN respectively. The outside machine will be the firewall's deft gateway and vice versa. Otherwise, configuration is almost exactly as described earlier.

When the firewall is working as you require, insert it into your live network, and continue as with step 8 above.