# # Tuning Production Systems

Unlike development tuning, the “Performance Tuning Principles” that Oracle recommends for production systems focus on more general techniques to identify and resolve tuning issues. Oracle outlines these principles in Chapter 22, “Instance Tuning,” of the Database Performance Guide and Reference Release 1 (9.0.1) documentation (Part Number A87503-02). They are also summarized in Table 1.2.

![](bbox=[0.17, 0.28, 0.24, 0.34])

The full library of Oracle documentation is available online at Oracle’s free Technet website: http://technet.oracle.com. This site also features trial software downloads and helpful user forums.

**TABLE 1.2** Oracle’s Production Performance Tuning Principles
| Priority | Description |
| --- | --- |
| First | Define the problem clearly and then formulate a tuning goal. |
| Second | Examine the host system and gather Oracle statistics. |
| Third | Compare the identified problem to the common performance problems identified by Oracle in the Oracle9i Database Performance Methods Release 1 (9.0.1) documentation (Part Number A87504-02). |
| Fourth | Use the statistics gathered in the second step to get a conceptual picture of what might be happening on the system. |
| Fifth | Identify the changes to be made and then implement those changes. |
| Sixth | Determine whether the objectives identified in step one have been met. If they have, stop tuning. If not, repeat steps five and six until the tuning goal is met. |