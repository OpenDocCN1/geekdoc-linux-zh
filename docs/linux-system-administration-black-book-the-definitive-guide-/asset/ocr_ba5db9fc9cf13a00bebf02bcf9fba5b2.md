Utilizing **cron** involves understanding how to represent time for a **cron** job, which is significantly different from how you do so with an **at** job. A **cron** time statement breaks down into the following parts:

A H D M W

Each one of these items is represented numerically, so **cron** needs placeholders even if you are not going to use the item. The entries for a **cron** time statement are listed in Table 23.2.

The possibilities get more complex from here. You have a choice of operators that you can use to express ranges and other items that allow you to express multiple time values for your **cron** job. These operators are explained in Table 23.3.

> **NOTE:** You can actually mix and match the dash and the comma operators; for example, `1,3,5-10,11,13`

# ## Search Tools

Few would argue that modern Linux is a large operating system. A standard workstation installation might span 850MB, and a server installation might need 1.7GB! The space needed by Linux and its associated tools, games, and more

**Table 23.2** Entries used in a *cron* time statement.

| Entry | Purpose | Value Range |
| :--- | :--- | :--- |
| A | Specifies the number of minutes after the hour | 0 through 59 |
| H | Specifies the hour, in 24-hour time | 0 through 23 |
| D | Specifies the date, or day of the month | 1 through 31 |
| M | Specifies the month of the year | 1 through 12, or the first three letters of the month name |
| W | Specifies the day of the week | 0 (Sunday) through 6 (Saturday), or the first three letters of the day name |

**Table 23.3** Operators available in a *cron* time statement.

| Operator | Purpose | Example |
| :--- | :--- | :--- |
| `*` | Specifies all possible values | `*` |
| `-` | Specifies the range of values between and including those on either side of the dash | `Mon-Fri` |
| `,` | Specifies the individual values listed | `1,3,5` |
| `/` | Specifies steps a group of values should follow instead of incrementing by 1 | `*/4` |