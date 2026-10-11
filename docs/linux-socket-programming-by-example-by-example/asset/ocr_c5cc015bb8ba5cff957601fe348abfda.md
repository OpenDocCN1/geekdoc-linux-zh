# ## Appendix A

# # Socket Function Quick Reference

# ## Socket-Specific Functions

**socketpair(2)**

    #include <sys/types.h>
    #include <sys/socket.h>
    
    int socketpair(int domain, int type, int protocol, int sv[2]);

**socket(2)**

    #include <sys/types.h>
    #include <sys/socket.h>
    
    int socket(int domain, int type, int protocol);

**bind(2)**

    #include <sys/types.h>
    #include <sys/socket.h>
    
    int bind(int sockfd, struct sockaddr *my_addr, int addrlen);

**connect(2)**

    #include <sys/types.h>
    #include <sys/socket.h>
    
    int connect(int sockfd, struct sockaddr *serv_addr, int addrlen);

**listen(2)**

    #include <sys/socket.h>
    
    int listen(int s, int backlog);