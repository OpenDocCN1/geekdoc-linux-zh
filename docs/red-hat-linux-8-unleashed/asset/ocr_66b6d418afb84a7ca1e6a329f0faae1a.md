554 CHAPTER 17 Administering Database Services in Red Hat Linux

In the example shown in Figure 17.1, the database contains only a single table. Most RDBMS setups are more complex than this, with a single database containing multiple tables. Figure 17.2 shows an example of a database named sample_database that contains two tables.

# sample_database

| last_name | first_name | phone |
| --- | --- | --- |
| Doe | John | 555-555-1212 |
| Doe | Jane | 555-555-1212 |
| Palmer | John | 123-456-7890 |
| Johnson | Richard | 111-222-3333 |

# serengeti_mammal

| common_name | order | family | genus | species | sub-species |
| --- | --- | --- | --- | --- | --- |
| African Lion | Carnivora | Felidae | Panthera | leo | |
| African Elephant | Proboscidea | Elephantidae | Loxodonta | africana | |
| Meerkat | Carnivora | Viverridae | Suricata | surricatta | |
| Hyena | Carnivora | Hyaenidae | Crocuta | |
| Reticulated Giraffe | Artiodacta | Giraffidae | Giraffe | camelopard | reticulata |
| Grant's Zebra | Perissodactyla | Equidae | Equus | burchell | |
| Cheetah | Carnivora | Felidae | |cinonyx | jubatus | |
| Thompson's Gazelle | Artiodacta | Bovidae | Gazella | thomsoni | |
| Hippopotamus | Artiodacta | Hippopotamai | Hippopotamus | amphibius |

FIGURE 17.2 A single database can contain two tables—in this case, phonebook and serengeti_mammal.

In the sample_database example, the phonebook table contains four records (rows), and each record holds three fields (columns) of data. The serengeti_mammal table holds nine records, divided into six fields of data.

If you are thinking there is absolutely no relationship between the phonebook table and the serengeti_mammal database, you are absolutely correct. In a relational database, users can store multiple tables of data in a single database—even if the data in one table is unrelated to the others.

For example, suppose you run a small company that sells widgets, and you have a computerized database of customers. In addition to storing each customer's name, address, and phone number, you would be able to look up outstanding order and invoice information for any of your customers. You could use three related tables in an RDBMS to store and organize customer data for just those purposes; Figure 17.3 shows an example of such a database.