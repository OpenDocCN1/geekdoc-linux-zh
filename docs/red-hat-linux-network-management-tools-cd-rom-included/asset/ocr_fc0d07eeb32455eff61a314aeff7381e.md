# Monitor Variable

One of the most important tasks that **tkined** has to offer is the ability to monitor one or more specific MIB objects. Selecting the Monitor Variable option displays a dialog window that permits the user to enter an MIB object name, as shown in Figure 11.46.

![](bbox=[0.21, 0.24, 0.8, 0.36])

*Figure 11.46 Monitor dialog window.*

You can add any valid MIB object name to this text box. Selecting the *start* button creates a graph on the topology view with the values of this object. In Figure 11.46, the MIB-II object *ifInOctets.4* was entered. Recall from Chapter 6, “Overview of MIB-II,” that this object contains the total number of incoming bytes for that the fifth interface on the system. Once **tkined** starts to monitor this object, a historical graph can be maintained to show the amount of network traffic going into this interface. Figure 11.47 shows a sample stripchart that tracks the *ifInOctets.4* object.

![](bbox=[0.17, 0.63, 0.47, 0.71])

*Figure 11.47 Stripchart of the ifInOctets object.*

# Interface Load

This option provides a stripchart for each interface within the target system. It is useful for viewing all the interfaces of a particular set of devices at the same time.

# TCP Service User

This option provides a count of the users accessing or using a particular TCP service. It is a good way to capture heavy use of cer-