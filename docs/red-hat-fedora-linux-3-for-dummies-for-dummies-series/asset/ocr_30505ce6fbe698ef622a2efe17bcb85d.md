+   11. Choose File::Save and click the OK button.
+   
+   Before you click OK, an Information window pops up, telling you that your changes have been saved and that you need to restart your network or computer to make them take effect. Then you return to the Network Configuration window.

+   12. Click the Activate button and your new Ethernet NIC turns on.

+   13. Choose File::Quit to close the Network Configuration window.
+   
+   You have created and saved the configuration necessary to use your cable modem. You have also activated that connection. You can start using your broadband Internet connection. Open Mozilla, for example, and start browsing at lightning speed.

![](bbox=[0.07, 0.35, 0.19, 0.45])

We strongly advise protecting your Internet connection with either the default firewall — installed automatically during the general installation process — or the one we describe in Chapter 8. The default firewall is automatically configured and run unless you choose not to install it (as described in Chapter 3) or explicitly turn it off. We prefer to install and use the more secure firewall from Chapter 8; nothing is wrong with the default firewall, but it’s less protective than ours. You can verify that your firewall is active by running the command service iptables status as root.

# # The DSL Option

We’re all wired — wired for telephones, that is. DSL modems take advantage of this old, common, appropriately named Plain Old Telephone Service (POTS) to provide a high-speed Internet connection to consumers. The DSL option uses special equipment to pump much more data through the POTS lines than a traditional analog modem does.

DSL provides high-speed Internet connections by electronically converting your computer’s digital network communications into a form that can be transmitted over the telephone company’s POTS. When your data finds its way to the telephone company, it’s converted into another form and forwarded to your ISP.

![](bbox=[0.07, 0.78, 0.19, 0.88])

DSL uses frequencies in the millions of cycles per second — the megahertz (MHz) range — compared to traditional analog modems, which work with signals in the thousands of cycles per second — kilohertz (KHz). You get much higher communication speeds when you use higher frequencies. Unfortunately, the telephone system wasn’t designed to work with higher frequencies.

Fortunately, the brainiacs of the world have figured out how to get high-speed DSL connections from the old, slow POTS. They have designed new digital signal-processing chips to overcome some of the POTS architecture limitations. The result is that if you live close enough — roughly three to four miles — to your DSL provider’s equipment, you can use DSL to get connected to the Net.