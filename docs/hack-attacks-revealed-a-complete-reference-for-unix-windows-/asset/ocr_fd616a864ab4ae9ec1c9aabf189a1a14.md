In order to communicate with other NetBIOS stations, a NetBIOS station must resolve its own name; it can have multiple individuals or group names (see Figure 2.11 for a real-world NetBIOS naming scenario).

# ### General, Naming, Session, and Datagram Services

To communicate across the network, a station’s applications can request many different types of NetBIOS services, including:

# **GENERAL SERVICES**

+   *   **Reset.** Used to free up resources into the NetBIOS pool for use by other applications.
+   *   **Status.** Includes sending/receiving station NIC status.
+   *   **Cancel.** Used to cancel a command.

![](bbox=[0.1, 0.32, 0.65, 0.5])

+   *   **Alert.** Issued to turn on NIC soft error notification for a specified time.
+   *   **Unlink.** Backward compatibility.

# **NAMING SERVICES**

+   *   **Add Name.** Used to add a name to NetBIOS.
+   *   **Add Group.** Used to add a group to NetBIOS.
+   *   **Delete Name.** Used to delete names and groups.
+   *   **Find Name.** Used to search for a name or group.

# **SESSION SERVICES**

Basically, establishes and maintains a communication session between NetBIOS stations based on user-assigned or NetBIOS-created names.

# **DATAGRAM SERVICES**

Used when NetBIOS wants to send transmissions without a required response with datagram frames. This process frees an application from obtaining a session by leaving the transmission up to the NIC. Not only is this process an unreliable delivery service, but it also is limited in data size: Datagrams will allow only up to 512 bytes per transmission. Datagram service commands include: