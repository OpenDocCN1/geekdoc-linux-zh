Automatic Undo Management (also known as System-managed Undo) is designed to minimize undo segment performance problems by dynamically managing the size and number of undo segments. This concept is similar to the dynamic management of sort segments in temporary tablespaces. With AUM, dedicated tablespaces, called Undo Tablespaces, are created to hold before-image data. The number and size of these undo segments is automatically managed by Oracle based on the demands of the system. The following sections describe techniques for using this new feature to improve undo segment I/O.

# Oracle Objective

Explain the concept of automatic undo management

# Configuring Automatic Undo Management

In order to utilize AUM in your database, you must first set four init.ora parameters to appropriate values. Descriptions of these parameters are included below.

+   **UNDO_MANAGEMENT** Used to indicate whether automatic (AUTO) or manual (MANUAL) undo management is being used in the database. The default is MANUAL.

+   **UNDO_TABLESPACE** Specifies the name of the tablespace where the AUM undo segments are to be stored. The default value is the first undo tablespace found during database startup.

![](bbox=[0.18, 0.66, 0.26, 0.71])

If no undo tablespace exists, the *SYSTEM rollback segment will be used to store undo data.*

+   **UNDO_RETENTION** Specifies (in seconds) how long to retain undo information after the transaction that generated it, commits. The default value is 900 seconds. This parameter is designed to help minimize *Snapshot Too Old* errors caused when a transaction needs overwritten before-image data for read consistency.

![](bbox=[0.18, 0.87, 0.26, 0.92])

Undo data can only be retained up to the time specified by *UNDO_RETENTION when adequate space has been allocated to the undo tablespace.*