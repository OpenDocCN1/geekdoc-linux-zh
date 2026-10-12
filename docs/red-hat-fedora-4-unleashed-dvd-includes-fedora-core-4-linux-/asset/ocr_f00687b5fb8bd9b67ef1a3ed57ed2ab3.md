locally or remotely over a network. Your responsibilities might include installing and maintaining these client programs on users' systems. This chapter discusses how to install and work with the clients from both the Linux command line and through its graphical interface database tools.

+   - **Managing accounts and users**—Account and user management include adding and deleting users from the database, assigning and administering passwords, and so on. In this chapter, you will learn how to grant and revoke user privileges and passwords for MySQL and PostgreSQL while using Fedora.

+   - **Ensuring database security**—To ensure database security, you need to be concerned with things such as access control, which ensures that only authorized people can access the database, and permissions, which ensure that people who can access the database cannot do things they should not do. In this chapter, you will learn how to manage Secure Shell (SSH), web, and local GUI client access to the database. Planning and overseeing the regular backup of an organization's database and restoring data from those backups is another critical component of securing the database.

+   - **Ensuring data integrity**—Of all the information stored on a server's hard disk storage, chances are the information in the database is the most critical. Ensuring data integrity involves planning for multiple-user access and ensuring that changes are not lost or duplicated when more than one user is making changes to the database at the same time.

# # A Brief Review of Database Basics

Database services under Linux that use the software discussed in this chapter are based on a *client/server* model. Database clients are often used to input data and to query or display query results from the server. You can use the command line or a graphical client to access a running server. Databases generally come in two forms: flat file and relational. A *flat file* database can be as simple as a text file with a space, tab, or some other character delimiting different parts of the information. One example of a simple flat file database is the Fedora `/etc/passwd` file. Another example could be a simple address book that might look something like this:

Doe-John-505  Some Street-Anytown-NY-12345-555-555-1212

You can use standard Unix tools such as grep, awk, and perl to search for and extract information from this primitive database. Although this might work well for a small database such as an address book that only one person uses, flat file databases of this type have several limitations:

+   - **They do not scale well**—Flat file databases cannot perform random access on data. They can only perform sequential access. This means they have to scan each line in the file, one by one, to look for specific information. As the size of the database grows, access times increase and performance decreases.