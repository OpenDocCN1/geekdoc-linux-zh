to recognize the next variant that is certainly coming in the future.

You can download a .pcap capture of the EternalBlue exploit here on Dropbox.

Download eternalblue-success-unpatched-win7-1.pcap from Dropbox here .

If you are unfamiliar with the Microsoft implementation of SMB (even most experts are not) and want to learn more, Microsoft has an excellent reference here.

Once the pcap file loads into Wireshark, go to packets 6 and 7. Here you see the protocol (SMB) negotionation. You should see a **Negotiate Protocol Request** and **Negotiate Protocol Response packets** .

These two packets are initiating the SMB protocol communication.



![](bbox=[0.12, 0.59, 0.87, 0.88])