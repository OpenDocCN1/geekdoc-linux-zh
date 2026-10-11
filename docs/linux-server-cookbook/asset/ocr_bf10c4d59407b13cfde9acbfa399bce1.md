| DECIMAL | An exact fixed-point number. |
| DATE | For date values. |
| TIME | For time values. |
| TIMESTAMP | For time and date together. |

Table 11.1: Column types and descriptions

A table can define which column or columns are going to be used as *Primary Key*. This *Primary Key* is going to be used to define a unique value between the rows. This key can be a column with data that will be unique (for example, the ID card of a student table), or it can be a column that will autogenerate a unique value. Only one primary key can be defined in a table. *Figure 11.2* features an example of a Primary key:

![](bbox=[0.25, 0.38, 0.75, 0.65])

*Figure 11.2: Primary key example*

A *Primary Key* cannot be blank and needs to be unique in the table. Other columns in the table can be optionally defined as *Unique Key* or as *Foreign Key*:

+   - **Unique Key:** This does not allow to have duplicated values in the column. For example, a phone number should be unique in a table of students. A table can have several *Unique Keys*. Refer to *figure 11.3*:

![](bbox=[0.18, 0.86, 0.82, 1.0])