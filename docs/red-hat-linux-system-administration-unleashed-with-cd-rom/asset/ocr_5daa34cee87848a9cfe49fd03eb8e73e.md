# The Production Network

The idea behind the production network is the same as for the administrative network, except that the base template is thinner. This allows you to create the various thin servers for the production network with minimal work.

For example, the Web server becomes simply a matter of taking the basic template for production servers and adding Web serving software and the documents to be served. You could also add limitations to the configuration to restrict access to this class of machines to port 80 only.

The same holds true for the other classes on the production network, such as the database servers and the mail servers. By creating the class templates, you can mix and match services on top of the base operating system template, thus reducing installation time and making maintenance much easier.

# An Implementation Example

To implement a class-based template scheme such as described is not as difficult as it may sound. Here are the steps needed to implement such a scheme:

+   1. Create the base template and installation method.
+   2. Create the class templates.
+   3. Create a distribution method for the class template.

The first step of this plan could be implemented using the homegrown approach described earlier in this chapter. With this method in place, the battle is more than half won.

The second step is to create the class templates. One method of doing this is to create a directory hierarchy such as shown in Listing 3.5.

# LISTING 3.5 Sample Directory Hierarchy for Class-based Template

```
|-- Db
|   |-- etc
|   |   |-- rc.d
|   |   |   |-- init.d
|   |   |   |   |-- database
|   |   |-- rc5.d
|   |   |   |-- K01database -> ../init.d/database
|   |   |   |-- S99database -> ../init.d/database
|-- services
|-- usr
```