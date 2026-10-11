# # CHAPTER 11
## Databases

# ## Introduction

A database is an organized collection of data stored electronically in a computer system. This database is controlled by a **database management system (DBMS)**. The data, the DBMS, and the applications associated are referred to *database system*. Applications use databases to store data in databases to be able to retrieve when required. This chapter will introduce to the basics of databases and the differences between relational and **non-relational (NoSQL)** database solutions.

The language **Structured Query Language (SQL)** is used in all relational databases. This chapter will explain how to query data, insert, and modify data inside a relational database. Different examples will be covered to demonstrate the usage of this language.

This chapter will focus on **MariaDB** as one of the most popular open-source relational databases. It will cover installation, configuration, backup, and restore for the service. It will also go over the process for the client to access the service and how to manipulate the data, such as creating databases, tables, and inserting data. A lightweight solution library database called **SQLite** will be covered.

For NoSQL, the database named **MongoDB** will be explained. This chapter will cover the installation and review the configuration. Access and manipulation of the data as a client will be described.

# ## Structure

In this chapter, we will discuss the following topics:

+   - Relational databases
+       - Structured Query Language (SQL)
+       - MariaDB server
+           - MariaDB client and tasks
+       - SQLite
+       - NoSQL databases