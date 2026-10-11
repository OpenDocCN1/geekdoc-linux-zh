```
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <stdlib.h>
#include <stdio.h>
#include "helper.h"
int main(void)
{
 int sockfd, infd; /* File descriptors for socket */
 struct sockaddr_in srv; /* Server's socket structure*/
 socklen_t socklen;

 /* Create the socket */
 if((Sockfd = socket(PF_INET, SOCK_STREAM, 0)) < 0)
 err_quit("socket");

 /* Initialize and set up the server structure */
 memset(&srv, 0, sizeof(srv));
 srv.sin_family = AF_INET;
 srv.sin_port = htons(50000);

 /* Bind the socket to an address */
 socklen = sizeof(srv);
 if((bind(sockfd, (struct sockaddr *)&srv, socklen)) < 0)
 err_quit("bind");

 /* Wait for incoming connections */
 if((listen(sockfd, 5)) < 0)
 err_quit("listen");
 puts("TCP/IP socket available");
 printf("\tport %d\n", ntohs(srv.sin_port));
 printf("\taddr %s\n", inet_ntoa(srv.sin_addr));

 /* Accept the first connection that comes in */
 if((infd = accept(sockfd, (struct sockaddr *)&srv, &socklen)) >= 0)
 puts("new connection granted");
```