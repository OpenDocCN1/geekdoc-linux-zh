Secure chat with SSH uses the SSH server as the chat server also. So when users connect to the SSH server and gain access to a shell, they can execute their IRC client on the SSH shell and be connected to the IRC server, which is running locally on the SSH server. Once the user is connected, he will have a chat session under his SSH shell, which is all encrypted over the network. Complete the following steps to create a secure chat solution with SSH and your favorite IRC server:

+   Install SSH on 172.16.6.100.
+   Install your favorite IRC server on 172.16.6.100.
+   Create accounts for all three users on the chat server, including Kusum, Shreya, and Neeraja.

> **NOTE** In larger networks, NIS+ can be used instead of creating local accounts for every IRC client.

+   With any of the three user accounts listed previously, connect to the SSH server using an SSH client.
+   Once authenticated, use an IRC client on the SSH server to connect to the local IRC services on the system.

Once you have logged in to the IRC server with the IRC client, running on the SSH server via your SSH client, you now have the ability to use IRC security with SSH. Your SSH terminal will show your IRC session with other accounts.

While this example is short and sweet, it is used to illustrate how an operating system running insecure services that are command-line-based, such as most IRC servers, can deploy an instance of SSH to make the connection secure. While the insecure service will still be available locally to all users, connections to and from the service will be allowed only with SSH, thus securing the connection over the network but still allowing access to the program locally. Figure 8.13 shows the two architectures.