# Removing Hosts

Removing hosts is just as simple as adding them. The actions described previously for adding hosts are reversed and executed in reverse order. I assume the host has already been physically disconnected from the network before removing it, so no more links are open to the host.

First, the host is removed from the nntp_access file so it can no longer access the news spool. This is done by function delnews law in Listing 16.1. Then, the information is removed from the named configuration and the named program is notified by the HUP signal. When both of these tasks are completed successfully, root is notified of the successful deletion. Root must check the routing information by hand to make sure no excess routes are left lingering in the kernel.

# Conclusion

The program presented in this chapter is experimental and is not suited for use in a production environment. You will need to tune it and add more error handling to deal with user and system errors. This program does show you the techniques involved and how to apply them in your own programs. Combining all of these simple steps into one program can save a lot of manual work and creeping errors.