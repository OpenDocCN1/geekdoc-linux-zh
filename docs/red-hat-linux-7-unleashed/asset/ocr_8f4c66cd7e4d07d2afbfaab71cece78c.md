To answer these questions, a few more questions might be necessary concerning the following areas:

+   - Accountability
+   - Change control and tracking
+   - Data integrity, including backups
+   - Physical security
+   - Privacy of data
+   - System access
+   - System availability

A more detailed plan can be developed based on discussion of these topics. As always, there will trade-offs; for example, privacy of data could mean that only certain people can log on to the system, which affects system access for the users. System availability is always in conflict with change control. For example, when do you change that failing hard drive on a 24/7 system? The bottom line is that your detailed plan should include a set of goals, a way of tracking the progression of the goals (including changes to the system), and a knowledge base of what types of tools are needed to do the job.

# ### Security Tools

Having the right tools always makes the job easier—especially when you are dealing with security issues. A number of tools are available on the Internet, including tools that check passwords and system security and protect your system. Some major UNIX-oriented security organizations assist the UNIX/Red Hat Linux user groups in discussing, testing, and describing tools available for use. CERT, CIAC, and the Linux Emergency Response Team are excellent sources of information for both beginning and advanced system administrators.

The following list introduces many of the available tools. This should be a good excuse, however, to surf the Net and see what else is available.

cops | A set of programs; each checks a different aspect of security on a UNIX system. If any potential security holes do exist, the results are either mailed or saved to a report file.
courtesy | A *satan* detector. *courtesy* gives the system administrator an early warning of possible network intrusions by detecting and identifying *satan*''s network probing.
crack | A program designed to find standard UNIX eight-character DES-encrypted passwords by standard guessing techniques.
deslogin | A remote *login* program that can be used safely across insecure networks.