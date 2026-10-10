# ## dbExpress Datasets Are Read-Only

dbExpress datasets are a read-only view into the underlying data in a database. No editing features are directly supported by dbExpress datasets, so any attempt to edit a dbExpress record results in a Delphi exception, as shown in Figure 2.1.

![](bbox=[0.31, 0.24, 0.59, 0.34])

**FIGURE 2.1**  
*dbExpress datasets are read-only.*

# ## dbExpress Datasets Are Lightweight

Because dbExpress datasets are unidirectional and read-only, they are extremely lightweight. There is no overhead involved for the fundamental (but expensive) tasks of bidirectional cursor support, record buffering, and the like.

If you're familiar with the *Borland Database Engine* (*BDE*), you know that the BDE supports full editing capabilities, forward and backward navigation of datasets, and drivers for multiple database backends. However, the BDE install is approximately 10MB, and the BDE itself is memory-intensive. Consider that dbExpress (when coupled with client datasets, which I'll discuss in future chapters) consists of a mere two library files totaling some 400K. Consider further that dbExpress (with client datasets) supports even more functionality than the BDE, and you begin to appreciate why dbExpress is such a remarkable database technology.

# ### Types of Datasets

As with other Delphi database technologies (such as ADO and IBX), dbExpress supports three different types of datasets: tables, queries, and stored procedures. These are discussed in the following sections.

# ### Tables

A table is a direct view of the underlying database table. It consists of all columns for all rows in the table. You cannot limit the rows returned from the table, and you cannot select a subset of columns (or join columns from another table).