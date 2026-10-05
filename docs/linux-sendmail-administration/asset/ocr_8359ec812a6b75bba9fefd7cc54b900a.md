# In Sum 105

masqueraded. The EXPOSED_USER command is used to define the usernames that should not be masqueraded.

Masquerading is covered extensively in Chapter 9, “Special m4 Configurations.” There are several more m4 commands that relate to masquerading, all of which will be covered in that chapter.

The commands in Table 4.1 and Table 4.3 are just the tip of the m4 iceberg. Many more commands are covered in Part 2 of the text as examples of advanced configurations, and all of the m4 commands are covered in Appendix A. This chapter does not exhaust coverage of the m4 language. It is an introduction to m4 that helps you understand the m4 commands contained in the sample files. Understanding these basic commands should help you read the macro configuration file provided by your vendor, which is a topic to tackle in Chapter 5, “Understanding a Vendor’s Configuration.”

![](bbox=[0.923, 0.256, 0.998, 0.383])

# In Sum

Sendmail reads its configuration from the sendmail.cf file. However, this file is not directly configured by the Sendmail administrator. Instead the file is constructed directly from m4 macros.

The Sendmail distribution provides the m4 source files needed to build a Sendmail configuration. The m4 source files are contained in the nine subdirectories of the cf directory. For most configurations, eight of the nine subdirectories can be ignored because they are either unused or contain source files that are never modified by the system administrator. The only subdirectory that the administrator needs to work with for most configurations is the cf/cf directory.

The cf/cf directory contains the macro configuration files. The Sendmail administrator creates a macro configuration file that selects the source files that provide the features necessary for the Sendmail configuration. Most macro configuration files are not built from scratch. The Sendmail distribution provides about 20 sample macro configuration files. You select a macro configuration file that matches your needs and make small adjustments if they are necessary.

The macro configuration file is processed through m4 to produce the sendmail.cf file. But even this step may not be necessary if you don’t need to change the sample macro configuration file for your configuration. Several Sendmail configuration files built from sample macro configuration files are included in the cf/cf directory.

To select and modify the correct macro configuration file, you must have a basic understanding of the m4 Sendmail macro configuration language. Use the tables in this chapter and the list of configuration commands in Appendix A to help you and modify the