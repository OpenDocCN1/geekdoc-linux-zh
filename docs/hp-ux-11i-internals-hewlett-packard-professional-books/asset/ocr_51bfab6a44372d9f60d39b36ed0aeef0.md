![](bbox=[0.2, 0.1, 0.95, 0.5])

# **Figure 3-5 Hash tables and Chains**

If your list had 100 names in it and your were looking for *Fred Flintstone*, the system would first total the character count (*Fred* has 4 and *Flintstone* has 10, a total of 15 counting the space between the names), which would send us to `hash[5]`. This entry would point to a name whose hash count is 5: if this were not the *Fred Flintstone* entry, you would simply follow the embedded hash-chain pointer until you found Fred’s entry (or reached the end of the list and failed the search).

If there were 100 entries in the table and 10 entries in the hashtable, using a standard distribution, then each hash chain would have 10 entries. On average, you would have to follow an individual chain for half of its length to get the data you wanted. That would be a five-linkage pointer search in our example. If we had to perform a sequential search on the unordered data, the average search length would have been 50 elements!* Even considering the time required to perform the hash calculation, this could result in considerable savings.

While this example is greatly simplified, it does demonstrate the basics of hash-headers and hash chains to speed up the location of the “right” data structure in a randomly allocated data table.