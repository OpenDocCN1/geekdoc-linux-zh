# # CHAPTER 6

# ## Users and Groups

# ### Virtual Partitions and Users

Each Virtual Partition is like a separate server. This means that you have sep-
arate users in your respective Virtual Partitions. Any user-related informa-
tion that needs to be shared between Virtual Partitions would be done in the
same manner as sharing between physically separate servers. For instance,
you may want to have users have the capability to remotely login from one
Virtual Partition to another. You would accomplish this by setting up the
appropriate network files in each Virtual Partition just as you would with
separate servers (see Chapter 13 for Networking.) Figure 6-1 shows Virtual
Partitions and the relationship to users: