An NIM environment is composed of two system types: an NIM master and one or more NIM clients. An NIM master centrally orchestrates all the management functions for the NIM clients in the network. The master server must be a stand-alone workstation with sufficient storage resources to provide boot images and shared product object trees (SPOT) for all managed clients. The NIM master server must be installed with the AIX network and spmgr filesets required for NIM operation. There is only one NIM master per set of clients. NIM clients may be any mixture of diskless, stateless, and stand-alone workstations with network connectivity to the NIM master.

NIM supports three types of clients:

+   - **Stand-alone**  Machines with local copies of AIX and LPPs
+   - **Diskless**  Network filesystems, paging, and dump; bootstrap ROM for network boot
+   - **Stateless**  Network filesystems; local paging and dump; bootstrap ROM for network boot; better performance than diskless configuration

The AIX filesets that make up NIM support are bundled in bos.sysmg. The bos.sysmg.nim.master filesset is used to build the NIM master server. The bos.sysmg.nim.client filesset is installed on each of the stand-alone NIM clients. The filesets bos.sysmg.nim.spot is used to create SPOT filesylesets for NIM diskless and stateless client types.

The NIM master stores information required to identify each managed client and network type as an object in an ODM database. This is where most of the difficulty comes in managing a NIM environment. Commands are supplied to list, update, and verify NIM ODM objects and relationships; but in practice, fending with the ODM is not quite as straightforward as working with human-readable tables. The NIM master must maintain relationships that link machine objects to network objects, network objects to network objects (routing), and machine objects to machine objects. Common NIM commands used to update and verify NIM ODM objects and relationships include nimm, nimconfig, nimplclient, and lsnim.

My recommendation is that you use SMIT to configure and manage NIM; you can use the Web-based System Manager, but it is a java pig and is very slow to use. The SMIT panels do a much better job in reminding you of all the attributes that must be associated with NIM objects to ensure that proper object-to-object relationships are maintained. Go ahead and use lsnim to do a quick check of ODM contents, but use SMIT to do the rest. I'll use SMIT in the following treatment of setting up an NIM environment.

# **For Information and Support**

+   - 1-800-CALL-AIX
+   - 1-800-IBM-4FAX
+   - 1-800-237-5511