time. However, it can be difficult to profile an irregular or dynamic user base. Profiles that are defined
too broadly enable any activity to pass review, whereas profiles that are defined too narrowly may
inhibit user work.

# Executable Profiling

Executable profiling seeks to measure and monitor how programs use system resources with particular
attention to those activity cannot cannot be traced to a specific originating user. For example,
system services usually cannot be traced to a specific user launching them. Viruses, Trojan horses,
worms, trappers, and other such software attacks are addressed by profiling how system objects
and printers are normally not only by users, but also by other systems on the part
of users. In most conventional systems, for example, any program, including a virus, inherits all
the privileges of the user executing the software. The system is not limited by the principle of least
privelege to only those privileges needed to properly execute. This openness in the architecture permits
virus to surreptiously change and infect totally unrelated parts of the system.

Executable profiling enables the IDS to identify activity that might indicate an attack. Once a potential
danger is identified, the method of notifying the administrator, such as by network message or e-mail,
is specific to the individual IDS.

# IDS Components and Processes

Regardless of what IDS you select, all have certain components in common. It is important to
have a general understanding of these components. The following terms will familiarize you with basic
components and functions in all IDSs:

+   - An activity is an element of a data source that is interest to the operator.
- The administrator is the person responsible for organizational structure.
- A sensor is the IDS component that collects data and passes it to the analyzer for analysis.
- The analyzer is the component or process that analyzes the data collected by the sensor.
- An alert is a message from the analyzer indicating that an event of interest has occurred.
- The manager is the part of the IDS used to manage, for example a console.
- Notification is the process or method by which the IDS manager makes the operator aware of alert.
- The operator is the person primarily responsible for the IDS. This is often the administrator.
- An event is an occurrence that indicates a suspicious activity may have occurred.
- The data source is the raw information that the IDS uses to detect suspicious activity.