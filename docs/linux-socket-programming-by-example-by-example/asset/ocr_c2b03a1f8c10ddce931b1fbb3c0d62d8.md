![](bbox=[0.82, 0.1, 0.96, 0.2])

# ## Socket Types and Protocols

In Chapter 1, “Introducing Sockets,” you saw how the socketpair(2) function was used to create a pair of local sockets. In this chapter, you will also learn about the socket(2) function to create a socket. These two functions have the domain, the socket type, and the protocol ingredients in common.

This chapter will build on the previous chapters by primarily focusing on the socket(2) function call. This includes expanding upon the following:

+   - The domain argument
+   - The socket type argument
+   - The protocol argument