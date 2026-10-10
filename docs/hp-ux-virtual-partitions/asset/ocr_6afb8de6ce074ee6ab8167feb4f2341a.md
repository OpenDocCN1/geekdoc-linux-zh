# NIS for Managing Users

One of the most popular ways to manage user-related information in a distributed environment is the Network Information System (NIS). NIS provides a method for multiple systems to share a centralized database of password, group, and other optional databases such as services and/or hosts. By doing so, the administration of user accounts is simplified for both end-users and system administrators. You will also often hear NIS referred to as “Yellow Pages” or “YP”; in fact, most of the NIS commands begin with the letters “yp”.

NIS and other such technologies are required only in a distributed environment where users have to be managed on many systems. This is because changes in information, such as adding and removing users, must be disseminated to many systems. This is normally not required in a centralized environment, where only a small number of copies of such information must be maintained.

NIS on HP-UX is interoperable with Solaris and Sun-licensed NIS implementations, including Linux. Like most of these implementations, HP’s NIS is not implemented in C2 or Trusted System mode. Additionally, Microsoft-based operating systems such as Windows do not use or interoperate with NIS.

# What Does NIS Manage?

NIS can manage many different databases. We'll focus on the user password and group information. Table 6-2 is a list of some of the databases NIS can manage: