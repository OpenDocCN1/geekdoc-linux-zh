# ## Amazon Relational Database Service

As we’ve seen time and time again throughout this book, AWS takes care of many of the underlying details so that you can focus on your application. Amazon RDS handles much of the operational complexity associated with the creation and maintenance of a relational database. Despite this, everything that you already know about MySQL still applies. You can use your existing tools, code, data, and queries. In this section we’ll examine some key Amazon RDS and MySQL concepts, take a peek at the Amazon RDS programming model, and wrap up with a look at the Amazon RDS pricing model.

# ### Amazon RDS Concepts

Most of the operations involving Amazon RDS are centered around a **DB Instance**. You can create the DB Instance as a **Single-AZ** or as a **Multi-AZ Deployment** (recall that, as we saw in the section called “Availability Zone” in Chapter 2, AZ is short for Availability Zone, and that AWS is designed so that failures affecting one AZ will not affect the others). The Multi-AZ Deployment offers increased availability and durability by synchronously replicating database updates between multiple Availability Zones, with automatic failover to a standby in the event of a failure.$^{2}$

You must specify the DB Instance Class when you create a DB Instance. There are currently five DB Instance Classes, as shown in Table 9.1.$^{3}$Unlike EC2, which offers a choice of 32-bit and 64-bit instance classes, all of the RDS DB Instance Classes are 64-bit.