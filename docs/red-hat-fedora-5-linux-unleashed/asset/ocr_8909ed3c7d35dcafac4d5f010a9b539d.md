# # CHAPTER 22
# Administering Database Services

## IN THIS CHAPTER

+   * A Brief Review of Database Basics
+   * Choosing a Database: MySQL Versus PostgreSQL
+   * Configuring MySQL
+   * Configuring PostgreSQL
+   * Database Clients
+   * Reference

This chapter is an introduction to MySQL and PostgreSQL, two database systems that are included with Fedora. You'll learn what these systems do, how the two programs compare, and how to consider their advantages and disadvantages. This information can help you choose and deploy which one to use for your organization's database needs.

The database administrator (DBA) for an organization has several responsibilities, which vary according to the size and operations of the organization, supporting staff, and so on. Depending on the particular organization's structure, if you are the organization's DBA, your responsibilities might include the following:

+   * **Installing and maintaining database servers**—You might install and maintain the database software. Maintenance can involve installing patches as well as upgrading the software at the appropriate times. As DBA, you might need to have root access to your system and know how to manage software (refer to Chapter 7, “Managing Software”). You also need to be aware of kernel, file system, and other security issues.

+   * **Installing and maintaining database clients**—The database client is the program used to access the database (you'll learn more about that later in this chapter, in the section “Database Clients”), either locally or remotely over a network. Your responsibilities might include installing and maintaining these client programs on users' systems. This chapter discusses how to install and work with the clients from both the Linux command line and through its graphical interface database tools.