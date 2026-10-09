```
struct sockaddr_in addr;

addr.sin_family = AF_INET;
addr.sin_port = htons(5559);
inet_aton("127.0.0.1", &addr.sin_addr);
mysocket = socket(PF_INET, SOCK_STREAM, getprotobyname("IP"));
bind(mysocket, (sockaddr *)&addr, sizeof(addr));
listen(mysocket, 10);

struct sockaddr_in newaddr;
while(1) {
int newsock;
socklen_t addrlen;
newsock = accept(mysocket, (sockaddr *)&newaddr, &addrlen);

if(fork() == 0) {
char msg[512];
sprintf(msg, "Welcome to SimonServer v0.0");
send(newsock, msg, strlen(msg), 0);

while(1) {
char buf[256];
int size;
size = recv(newsock, buf, sizeof(buf), 0);
buf[size] = 0;
char buf2[512];
sprintf(buf2, "Simon says: %s", buf);
send(newsock, buf2, strlen(buf2), 0);
if(strncmp(buf, "quit", 4) == 0) {
send(newsock, "bye", 4, 0);
shutdown(newsock, 2);
exit(0);
}
}
}
close(mysocket);
}
```

# Running the Sample Server and Client

To run the client/server network program, first compile both the client and the server with **make**. Then, type **server**& **press Enter**. The ampersand causes the server program to run in the background. Next, type **client** and **press Enter**. You should see a brief welcome message from the server. Then, anything you type will be sent to the server, and the server will repeat what you typed to demonstrate that it received the data correctly. Try starting several instances of the client program in different windows. Notice how several clients can connect simultaneously. When you are done, you should kill the server. Determine its process number with the command **ps x**, and then type **kill PID**, where PID is the process number of the server process.

# Non-Blocking Operations

The socket operations as described above are blocking. That is, **accept** waits until a new connection is present before proceeding, **send** waits for the data to be completely transmitted before