```
```text
    printf("connect to server failed");
    exit(-1);
}

int ok = 1;
while(ok) {
    char response[1024];
    int response_len;

    response_len = recv(mysocket, response, sizeof(response),0);
    response[response_len] = 0;
    printf("server said: %s",response);

    char s[256];
    gets(s);
    printf("sending following string to server: %s",s);
    ok = ( send(mysocket, s, strlen(s),0) > 0 );
}
shutdown(mysocket,2);
```

```

In the sample program, we hard-coded the IP address and port number of the server. You can change these values to any valid Internet address and port number to connect to any machine reachable via the Internet Protocol. A server should be listening on the specified IP address and port number. For the purposes of this section, we are interested in creating our own server, so that our 3D programs can exchange data with one another in real time. Writing a server is our next topic.

# # The Server

Writing a simple IP server is not much more difficult than writing the client. We first declare an Internet address structure of type `sockaddr_in`, and fill it with the IP address and port of the *server*. In other words, the server fills the address structure with its own IP address, and with the port number on which it will be listening. In the sample program *server*, we specified address `127.0.0.1` for the local host, but in a real application with separate client and server machines, you would replace this with the actual IP address of the server machine in the network. The port number specified in the server should be the same as the port number in the client; otherwise no communication will be possible.

Note that one machine can have several IP addresses; indeed, an IP address is not assigned to a “machine,” but is instead assigned to a *network interface*, whereby one machine can have several network interfaces (such as network cards, and PPP modem interface). To allow incoming connections on any of the server machine's IP addresses, we can use the assignment `addr.sin_addr=sin_addr=INADDR_ANY`, where `INADDR_ANY` means that any IP address on any of the server's network interfaces will accept an incoming connection.

You obtain your IP address from your Internet service provider (ISP). If you use a dial-up connection to the Internet, then your IP address is probably dynamically assigned each time you connect to the Internet; if you have a cable modem, you probably have a static IP address which always stays the same. Putting servers on dynamic IP addresses requires the server to somehow announce its location to potential clients; one way is to have a WWW site with a static IP address,