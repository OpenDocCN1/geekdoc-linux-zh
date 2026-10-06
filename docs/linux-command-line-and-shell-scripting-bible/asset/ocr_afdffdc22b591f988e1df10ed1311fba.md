![](bbox=[0.1315, 0.1135, 0.9175, 0.365])

The master program is used to control the overall operation of Postfix. It is responsible for starting other Postfix processes as needed. The qmgr and pickup programs are configured to remain as background processes longer than other core programs. The pickup program determines when messages are available to be routed by the Postfix system. The qmgr program is responsible for the central message routing system for Postfix.

Table 26-3 shows other core programs that Postfix uses to transfer mail messages.

# The Postfix Core Programs

| Program | Description |
|--- | --- |
| bounce | Posts a log in the bounce message queue for bounced messages and returns the bounced message to the sender |
| cleanup | Processes incoming mail headers and places messages in the incoming queue |
| error | Processes message delivery requests from qmgr, forcing messages to bounce |
| flush | Processes messages waiting to be retrieved by a remote mail server |
| local | Delivers messages destined for local users |
| pickup | Waits for messages in the mailqueue and sends them to the cleanup program to begin processing |
| pipe | Forwards messages from the queue manager program to external programs |