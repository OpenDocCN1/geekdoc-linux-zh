Let’s examine how this works a bit more closely. Suppose a user at Three Room Company in Boston wants to access a computer at Guy in a Garage in Seattle. Here’s what happens:

+   1. Network traffic traverses Three Room Company’s networks until it reaches the machine that serves as the router between Three Room Company and its ISP.
+   2. The data does a similar traversal of the ISP’s network until it reaches the ISP’s router to its chosen Internet backbone. (Instead of a backbone, the traffic could travel first to a larger ISP, and perhaps from there to one that’s still larger. The number of these steps is generally called the number of hops to the backbone.)
+   3. After the data gets on a backbone, it travels to the nearest connection to the backbone that services Guy in a Garage and jumps to this second backbone. Of course, if both the source and destination computers use the same backbone, this step can be skipped.
+   4. The destination backbone sends the data to the ISP that services Guy in a Garage (or the ISP closest to the backbone in Guy in a Garage’s ISP hierarchy).
+   5. The ISP delivers the data to the router at Guy in a Garage.
+   6. Guy in a Garage’s router sends the data to its destination computer, possibly via additional routers, bridges, or other distribution means.

Figure 4.7 shows these steps graphically. In reality, each labeled stop on the trip from Three Room Company to Guy in a Garage could represent passage through several computers, however. This is particularly true at the backbone level, and at the ISP level when there are several tiers of ISPs between the customer and the backbone.

![](bbox=[0.15, 0.82, 0.75, 0.95])

FIGURE 4.7
Traffic between remote sites typically travels through half a dozen, a dozen, or more intermediate computers.