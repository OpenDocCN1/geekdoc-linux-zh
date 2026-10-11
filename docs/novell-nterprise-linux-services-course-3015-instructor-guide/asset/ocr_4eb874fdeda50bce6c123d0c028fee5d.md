Although these models are important to the X.500 specification, we will present a simple, condensed overview of the essential components of a Directory that cross the boundaries of several of these models.

# ## The Components of the X.500 Directory

Essential components of the X.500 standard include the following:

+   Directory Information Database (DIB)
+   
+   Directory Information Tree (DIT)
+   
+   Directory User Agent (DUA)
+   
+   Directory System Agent (DSA)
+   
+   Directory Access Protocol (DAP)
+   
+   Directory System Protocol (DSP)
+   
+   Directory Information Shadowing Protocol (DISP)

# ### Directory Information Database (DIB)

A Directory is made up of objects that represent physical resources in the real world. For example, people, servers, and printers are represented by objects in the Directory tree.

Collectively, these objects are known as the Directory Information Database (DIB).

Within the DIB each object is made up of a collection of information known as an *entry*. Each entry is made up of attributes and values and has a distinguished name that uniquely identifies the entry.