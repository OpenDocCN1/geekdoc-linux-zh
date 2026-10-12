# Advanced MySQL

One of the key elements of most dynamic websites is the database that feeds it. From a simple news page, to an elaborate publishing system or CMS, the database plays a central role in the management of a site’s content. To keep a site running smoothly, it helps to know a few tips and tricks of the database system. In this chapter, you’ll learn how to create your databases, manage the various user accounts that will access the system, and combine and optimize your SQL code to perform complex and intricate queries.

# The Basics, Revisited

Before tackling the more advanced features, here’s a quick review of MySQL usage. Pretend you’ve just landed a new client, a car dealership. The manager at the dealership wants you to create a web-site that will help them keep track of their car inventories. No problem, you say, and you sit down and begin planning out their web application.

During your planning, you come up with a simple multi-table database scheme to hold the data for their car lots. For the purposes of these exercises, you’ve decided to create database tables that resemble Figure 4.1.

What you’ve created is a very simple database structure that involves four tables. In the New_Vehicles table, you’ll be storing data for, obviously enough, new cars. Properties such as mileage, price, color, and description can be specified for each car in stock. The Used_Vehicles table has a nearly identical structure to New_Vehicles , but is designed to hold records for, as you might guess, used cars. The Used_Vehicles table has a couple additional columns provided to indicate whether the vehicle is certified or has a warranty, and a column for mileage. The last two tables, Makeand Model, store common make and model designations for the various brands the dealer sells.