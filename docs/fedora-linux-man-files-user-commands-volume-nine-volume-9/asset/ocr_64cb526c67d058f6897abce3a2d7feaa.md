login, and the user can thus use the privileges given by the identities anywhere in the network in a secure way.

There are two main ways to get an agent set up: The first is that the agent starts a new subcommand into which so environnt variables are exported, eg **ssh-agent xterm &** The second is that the agent prints the needed shell commands (either (1) or (1) syntax can be generated) which can be evaluated in the calling shell, eg `eval ‘ssh-agent -s’` for Bourne-type shells such as (1) or (1) and `eval ‘ssh-agent -c’` for (1) and derivatives.

Later (1) looks at these variables and uses them to establish a connection to the agent.

The agent will never send a private key over its request channel. Instead, operations that require a private key will be perford by the agent, and the result will be returned to the requester. This way, private keys are not exposed to clients using the agent.

A UNIX socket is created and the na of this socket is stored in the **SSH_AUTH_SOCK** environnt variable. The socket is made accessible only to the current user. This thod is easily abused by root or another instance of the sa user.

The **SSH_AGENT_PID** environnt variable holds the agent’s process ID.

The agent exits automatically when the command given on the command line terminates.