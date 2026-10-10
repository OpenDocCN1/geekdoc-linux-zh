# ## Creating a New Project

For our initial exercise in creating a C/C++ project, we will create a fairly straightforward record sorting application. The records to be sorted consist of a name and an ID number. To simplify the code a bit, we will replace any spaces in the name field with underscores. The program will sort a file of records in ascending order, either by name or ID number, as specified on the command line thus:

```
record_sort< datafile> [ 1 | 2 ]
```

where 1 means sort by name, and 2 means sort by ID. Sort by name is the default if no sorting argument is given.

In the Eclipse C/C++ perspective, select `File>New>C Project`. This brings up the New Project wizard shown in Fig. 5.4. Call it "record_sort." The project type is `Executable>Empty Project.` The tool chain is `Linux GCC`, and we will use the default workspace location. Clicking `Next` brings up the Select Configurations dialog, where you can select either or

![](bbox=[0.11, 0.52, 0.89, 0.85])

**Figure 5.3**  
Eclipse Welcome screen.