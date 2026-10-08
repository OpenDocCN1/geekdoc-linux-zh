IT/O provides more managed node capabilities, while NNM provides mostly monitoring capabilities through standards such as SNMP. With IT/O agents, you can do more than just monitor managed nodes. You can manage them, too. With IT/O, you can set up more sophisticated message conditions and configure automatic or operator-initiated actions to run on the managed nodes. IT/O also provides more flexibility to add additional monitoring to your managed nodes.

In both NNM and IT/O, colored icons on the graphical map are used to reflect node status. In NNM, node status is usually determined by the network status of the system, including the status of the network interface cards. In IT/O, node status is determined not only by the network status of the system, but also by the IT/O alarm status for that node.

# ## IT/O and PerfView

PerfView can be integrated into the IT/O Application Bank. With this integration, you can easily select a managed node, then use PerfView to graph metrics collected on the selected node. Add- tionally, templates can be configured so that if you receive a PerfView alarm condition in the IT/O Message Browser, you can run an operator-initiated action that will invoke PerfView to create a graph showing metrics related to the alarm condition.

If you have the MeasureWare Agent installed on an IT/O managed node, it will detect the IT/O agent running and automatically start sending alarms to it.

# ## BMC PATROL and IT/O

PATROL does not require a special management console. Instead, its server-based PATROL agents can send monitoring information via SNMP traps to management platforms such as HP OpenView NNM and IT/O, CA UniCenter TNG, and Tivoli TME. This level of integration requires an addi- tional product called PATROLVIEW, and there are special versions for OpenView, Cabletron SPEC- TRUM, Remedy AR, Sun's Solstice Domain Manager, and Tivoli TME. The PATROL product can be integrated with Unisenter TNG through a special product called PatrolLink.

You need to install PATROLVIEW on the IT/O management station. This process installs and sets up message groups, message templates, node groups, threshold monitors, and application icons.

One of the unique things about PATROL's integration with IT/O is that PATROL agents from many systems, not just IT/O managed nodes, can send events to IT/O. PATROLVIEW includes a PATROL Event Translator server, the PET server, which translates PATROL events in IT/O events. The PATROL agents send events to the PET server on the IT/O managed node. The PET server processes and forwards the events to the IT/O agent.

The PET server runs on one or more IT/O managed nodes. It receives and processes events from one or more PATROL agents, then forwards the data to the IT/O agent that processes the events and forwards them, if necessary, to the IT/O console. You can also install the PET server on more than one managed node. This is useful if one of your PET servers goes down. If you have only one PET server configured and it goes down, you will lose the connection to all of the PATROL agents that send events to the PET server and on to IT/O.