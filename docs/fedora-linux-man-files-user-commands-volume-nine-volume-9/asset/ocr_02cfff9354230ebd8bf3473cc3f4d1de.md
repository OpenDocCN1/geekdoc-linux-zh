Lists the **ORBId** of the ORBs defined on a server. An **ORBId** is the string na for the ORB created by the server. If the server is not already running, then it is activated.
`shutdown` *-serverid* *server-id* *-* *-applicationNa* *application-na*
Shut down an active server that is registered with ORBD. During execution of this command, the **shutdown** thod defined in the class specified by either the **-serverid** or **-applicationNa** parater is also called to shut down the server process.
`startup` *-serverid* *server-id* *-* *-applicationNa* *application-na*
Starts up or activate a server that is registered with ORBD. If the server is not running, then this command starts the server. If the server is already running, then an error ssage is displayed.
`help`
Lists all the commands available to the server through the **servertool** command.
`quit`
Exits the **servertool** command.