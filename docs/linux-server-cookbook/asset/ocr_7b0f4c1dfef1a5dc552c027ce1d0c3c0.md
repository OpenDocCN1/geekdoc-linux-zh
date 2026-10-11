+   - **Internal API:** Communication to the *Services API* between the services. For example, the **nova** service (responsible for computing) communicates with the **neutron** service (responsible for networking) using this network.

+   - **Tenant:** Used by the *Virtual Machines* in the east-west traffic (communication between *Virtual Machines*) and the north-south traffic (from or to outside the *cluster*).

+   - **Storage:** Traffic generated from and to the systems providing the storage to **OpenStack**.

+   - **Storage Management:** Traffic used internally between the systems involved in the *Storage* systems.

+   - **External:** Used to provide external access from outside the cluster. The *Network* is used to provide an external address to be used for *API*, *Web access*, and access to the instances running on **OpenStack**.

An additional network called **Management** can be configured to access the cluster nodes to be administrated, usually only accessible by the teams who administrate the cluster. *Figure 16.4* shows a network layout for **OpenStack**: