The Todos table stores reminders for each contact. For example, you might want to store a reminder to phone a certain contact on a given date to place an order. The Todos table and Contacts table are linked through the Todos table's ContactID field.

In addition to the tables, the database contains a stored procedure named contactsByState. This procedure is provided for use in the sample applications shown in Chapters 1 and 2; it won't be used in the ConMan application.

Finally, the script creates a generator used to populate the primary keys of the Contacts and Todos tables and two triggers that run when a new contact and todo are entered, respectively. The triggers ensure that new contacts and todos always receive a unique primary key.

# Listing 9.1 ConMan.SQL

```
/\* Table: CONTACTS, Owner: SYSDBA \*/

CREATE TABLE CONTACTS
(
    CONTACTID    INTEGER NOT NULL,
    FIRST         VARCHAR(20),
    LAST          VARCHAR(30),
    DEAR          VARCHAR(40),
    TITLE         VARCHAR(30),
    COMPANYNAME   VARCHAR(50),
    ADDRESS1      VARCHAR(50),
    ADDRESS2      VARCHAR(50),
    CITY          VARCHAR(30),
    STATE         VARCHAR(20),
    POSTALCODE    VARCHAR(10),
    COUNTRY       VARCHAR(30),
    PHONE         VARCHAR(20),
    FAX           VARCHAR(20),
    CELLULAR      VARCHAR(20),
    PAGER         VARCHAR(20),
    EMAIL         VARCHAR(40),
    IMAGE         BLOB SUB_TYPE 0 SEGMENT SIZE 4096,
    NOTES         BLOB SUB_TYPE TEXT SEGMENT SIZE 4096,
    PRIMARY KEY (CONTACTID)
);

CREATE UNIQUE INDEX IX_CONNAME ON CONTACTS (LAST, FIRST);

CREATE TABLE TODOS
(
```