![](bbox=[0.4, 0.09, 0.65, 0.105])

Relationships are a logical connection between different tables. A record (row) of one table can reference or be referenced by another record from a different table. There are three possible relationships:

+   * **One-to-one relationship (1:1):** One record can refer only to one element. For example, a country has only one capital city. Refer to figure 11.5:

# One-to-one relationship

![](bbox=[0.18, 0.305, 0.88, 0.43])

![](bbox=[0.4, 0.45, 0.65, 0.465])

+   * **One-to-many relationship (1:N):** A record can be referenced by many elements. For example, a country has several cities, but a city can only be part of one country. Refer to figure 11.6:

# One-to-Many relationship

![](bbox=[0.18, 0.615, 0.88, 0.785])

![](bbox=[0.4, 0.795, 0.65, 0.81])

+   * **Many-to-many relationship (M:M):** Several records can be referenced by many elements. For example, a country can have several official languages, and a language can be official in many countries. This case requires having an intermediate table to keep the relations. Refer to figure 11.7: