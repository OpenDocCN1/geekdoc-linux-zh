# 3

# NFS, NIS, AND RDIST

# 3.1 Introduction

NFS and NIS are often bunched together in many books. Functionally, they don’t have much to do with each other; they perform different tasks and for the most part work independently. Sure, you can use NIS maps in your NFS configuration, but you can use NIS maps almost anywhere. Still, they both send information from one machine to another, which makes it useful to discuss them together.

NFS (Network File System) is a means of mounting one machine’s filesystem on another. NIS (Network Information Service) performs a variety of mostly user-related stuff—centralized user accounting (passwd and group files) is its biggest function.

NFS and NIS are not perfect. NFS suffers from a variety of performance and design shortcomings, and both have an annoying habit of sending their information unencrypted over the network. Furthermore, if configured incorrectly, they can perform horribly and have deleterious effects on system stability. They are widely used in spite of their faults because you can find free implementations everywhere.

We present rdist as an alternative to NFS in some cases. NFS was once used for any filesystem of substantial size, including parts of the system installation, since disk space was far too expensive to keep a complete local copy of