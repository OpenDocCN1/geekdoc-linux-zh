Other applications may need to react to external events; for instance, they may send requests to some of their devices in response to information they have received from others. An illustration is the overheat detection sensor mentioned earlier: the application really needs to get the alarm notification from the heat sensor on time and react within the appropriate time frame to shut down the malfunctioning device, or the latter is likely going to be toast.

# The aerospace industry

This industry is a large consumer of real-time technology at various levels of its product development process, from the early design stage to its exploitation. For instance, Integrated Modular Avionics (IMA) is a blanket term used to describe a distributed real-time computer network aboard an aircraft. This network consists of a number of computing modules capable of supporting numerous applications involving various safety criticality levels.

Another typical use of real-time capabilities in this industry involves simulation systems with real hardware attached to it, an approach called *hardware-in-the-loop* (HIL) simulation. Real-time is needed here because portions of this software have to interact with the physical world. By making it possible to test new, actual devices in a virtual environment, this solution allows the designers to predict whether the overall airborne system will meet initial performance specifications, without actually having to build it for real in its entirety.

# The financial services industry

It is particularly interesting that even high-level online financial services could depend on basic real-time technology issues. As a matter of fact, some of the complex distributed applications that are critical to this business may have requirements for exchanging messages reliably and in a timely fashion.

For instance, when it comes to connecting trading systems to stock exchanges around the world, with hundreds of financial transactions taking place every minute, too much delay in processing trading opportunities within a handful of seconds could mean significant losses.

For this reason, trading systems are increasingly dependent on real-time response. The fact that such applications operate on a milliseconds timescale, instead of the microsecond one used by measurement and control systems, does not change their basic requirement for always being on time (i.e., for being real-time).

# The multimedia business

Generally speaking, multimedia systems have to process visual and auditive information in a time frame short enough for the audience not to perceive visible or audible artifacts. Such applications can allow some deadlines to be missed once in a while, but this should remain a rare case so that they maintain an overall good quality of service.