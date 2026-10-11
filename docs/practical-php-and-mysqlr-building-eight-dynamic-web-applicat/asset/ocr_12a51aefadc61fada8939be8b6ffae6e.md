# # BUILDING THE DATABASE

The database you will create is shown in Figure 6-1.

![](bbox=[0.12, 0.2, 0.88, 0.55])

FIGURE 6-1 The database schema revolves around the main *orders* table.

This entire project fundamentally hinges on orders stored in the *orders* table. This table relates to the *customers* (contains registered customer address details) and *delivery\_addresses* (contains unregistered and alternative addresses) tables. Each product (stored in the *products* table) in the order is stored in the *order\_items* table. Other tables include *logins* (stores the registered user's login details), *categories* (contains the categories that the products are part of), and *admins* (stores administrator login details).

# ## Implementing the Database

Start phpMyAdmin, create a new database called *shoppingcart*, and add the following tables: