**TIP** If no table name is specified with the STATTAB parameter, then the gathered system statistics will be stored in the data dictionary. Users who wish to store statistics in the data dictionary must have SYSDBA privileges.

**TIP** Oracle highly recommends that system statistics be gathered in order to improve the performance of the CBO.

**NOTE** For complete details of the many options available in the DBMS_STATS package, see Chapter 63, “DBMS_STATS,” of *Oracle9i Supplied PL/SQL Packages and Types Reference, Release 1 (9.0.1)* (Part Number A89852-02).

# ### Using the OEM Console to Gather Statistics

The OEM Console can also be used to gather schema statistics. By selecting Tools > Database Wizards > Analyze from the OEM Console menu, the Analyze Wizard show in Figure 3.8 will be displayed.

![](bbox=[0.1, 0.55, 0.87, 0.95])