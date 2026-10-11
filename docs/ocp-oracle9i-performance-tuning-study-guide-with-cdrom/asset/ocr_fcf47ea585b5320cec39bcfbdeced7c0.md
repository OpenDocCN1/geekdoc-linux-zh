42. Oracle recommends you use an OFA-compliant architecture when setting up your Oracle Server. What does OFA stand for?

+   A. Oracle Flexible Architecture

+   B. Oracle FailSafe Architecture

+   C. Optimal Flexible Architecture

+   D. Optimal FailSafe Architecture

43. The DBA wants to increase the size of the database buffer cache by 100MB. Currently, the overall size of the SGA is 256MB, the SGA_MAX_SIZE has been set to 300MB, and total system memory available to Oracle on the machine is 300MB. What should the DBA do?

+   A. Issue ALTER SYSTEM commands to dynamically modify the SGA_MAX_SIZE and DB_CACHE_SIZE.

+   B. Issue ALTER DATABASE commands to dynamically modify the SGA_MAX_SIZE and DB_CACHE_SIZE.

+   C. Shut down, change the SGA_MAX_SIZE and DB_CACHE_SIZE parameters, and restart the instance.

+   D. The DBA cannot increase the size of the database buffer cache by 100MB.

44. Which of the following would not be a characteristic of an SQL statement that may require further tuning?

+   A. A statement that consumes excess CPU resources

+   B. A statement that has a long parse, fetch or execute time

+   C. A statement that reads too many data blocks from the SGA and too few from disk

+   D. A statement that accesses many data blocks but returns only a few rows

45. You are setting up a new database. You have set up tempfiles to use for sorting and you would like to ensure that no users created in the database will use the system tablespace as their default temporary tablespace. What command could you issue to prevent this?