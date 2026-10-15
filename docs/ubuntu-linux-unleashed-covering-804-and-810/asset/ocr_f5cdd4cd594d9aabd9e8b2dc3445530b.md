# phonebook

| last_name | first_name | phone |
|---|---|---|
| Doe | John | 555-555-1212 |
| Doe | Jane | 555-555-1212 |
| Palmer | John | 555-123-4567 |
| Johnson | Richard | 555-111-4321 |

# cd_collection

| id | title | artist | year | rating |
|---|---|---|---|---|
| 1 | Mindbomb | The The | 1989 | 4 |
| 2 | For All You've Done | Hillsong | 2004 |  |
| 3 | Trouser Jazz | Mr. Scruff | 2002 | 5 |
| 4 | Natural Elements | Acoustic Alchemy | 1988 | 3 |
| 5 | Combat Rock | The Clash | 1982 | 4 |
| 6 | Life for Rent | Dido | 2003 | 5 |
| 7 | Adiemus 4 | Karl Jenkins | 2000 | 4 |
| 8 | The Two Towers | Howard Shore | 2002 | 5 |

FIGURE 21.2 A single database can contain two tables—in this case, phonebook and cd_collection.

phone number, you want to be able to look up outstanding order and invoice information for any of your customers. You could use three related tables in an RDBMS to store and organize customer data for just those purposes. Figure 21.3 shows an example of such a database.

# customers

| cid | last_name | first_name | shipping_address |
|---|---|---|---| 
| 0 | Doe | John | 505 Somestreet |
| 2 | Doe | Jane | 505 Somestreet |
| 3 | Palmer | John | 200 Anystreet |
| 4 | Johnson | Richard | 1000 Another Street |

# orders

| cid | order_num | stock_num | priority | shipped | date |
|---|---|---|---|---|---|
| 0 | 1002 | 100.252.342 | 3 | Y | 8/31/01 |
| 0 | 1221 | 200.352 | 1 | N | 10/2/01 |
| 3 | 1223 | 200.121 | 2 | Y | 10/2/01 |
| 2 | 1225 | 221.152 | 1 | N | 10/3/01 |

# overdue

| cid | order_num | days_overdue | action |
|---|---|---|---|
| 0 | 1002 | 32 | sent letter |

FIGURE 21.3 You can use three related tables to track customers, orders, and outstanding invoices.