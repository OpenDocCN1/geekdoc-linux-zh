# # 20
# Windows Networking –
# logon and domains

+   20.1	Overview of NT domains and security
+   20.2	The logon prompt and local and network logons
+   20.3	Local logon. Encrypting the password
+   20.4	Logon over the network – overview
+   20.5	Logon over the network (1a) – “discover” a domain controller
+   20.6	Logon over the network (1b) – the computer account
+   20.7	Logon over the network (1b contd) – PC authenticates and creates a secure channel
+   20.8	Logon over the network (2) – sending the password securely
+   20.9	Different logon types: terminology (1)
+   20.10	Different logon types: terminology (2)
+   20.11	Logon and controlling access to network resources
+   20.12	Domain controllers
+   Summary

# ## Introduction

This chapter explains how Windows Networking uses “domains” to control user logons and access to resources, and how in logging on to the domain your PC interacts over the network with a “domain controller,” which performs the actual validation of your logon.

We cover these topics in a lot of detail – certainly more than you need in day-to-day operations, (a) because it’s hard to get this information elsewhere, and (b) so that when something goes wrong you can understand what the error messages really mean and use an intelligent approach in resolving your problem. You can skip Modules 20.5–20.10 on first reading if you wish.