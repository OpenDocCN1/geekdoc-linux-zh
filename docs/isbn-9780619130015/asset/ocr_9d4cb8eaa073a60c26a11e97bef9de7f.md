# EXERCISES

+   1.  What is the advantage of using script files?
2.  What is the difference between join and paste?
3.  Why is the operation performed by the join command called a "relational join?"
4.  What two ways do you use to specify patterns and actions to the awk command?
5  Create a join script for the vendors and products files showing which products do not have a matching vendor record.
6.  Write a simple Awk program to print the phones1 file in Figure 4-3.
7.  Write a script file to display the vendor file, and then run the script.

# DISCOVERY EXERCISES

+   1.  Use vi, Emacs, or the method of your choice to create the files cust_names, cust_ids, and cust_status. The files should have the following contents.
    Contents of cust_names:
    Smith Furniture Co.
    Wells Manufacturing
    Rose Department Store
    Haywood Resort
    Contents of cust_ids:
    101
    102
    114
    197
    Contents of cust_status:
    ACTIVE
    ACTIVE
    INACTIVE
    ACTIVE
2.  Use the paste command to create a file named cust1. Combine the cust_ids and cust_names files to create cust1. Use the colon character as the field delimiter.
3.  Use the paste command to create a file called cust2. Combine the cust_ids and cust_status files to create cust2. Use the colon character as the field delimiter.
4.  Use the join command to join cust1 and cust2 and create the file cust_info. The key field is the first field of cust1 and cust2 (which lists the customer ID).
5.  Write an awk command that reads the cust_info and displays the customer IDs followed by the customer names. The customer IDs should be printed in a right-justified field of 10 spaces.