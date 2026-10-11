# # IN-DEPTH

# ## Programming Snapshot – Go Interfaces

![](bbox=[0.09, 0.11, 0.92, 0.52])

Figure 3: One GitMeta entry is all you need for all of a user’s GitHub repositories.

line 30, **FindPlugin** returns the reference found in this way to the caller, or it reports an error in line 33 if it failed to find a suitable plugin.

The **G**MF parser in Listing 2 is now object-oriented itself; line 36 defines its constructor. As the instance data, the **GitMeta** structure in line 13 contains an array slice of **Cloneable** types, each of which contains repositories to be cloned into their target directories (**Figure 2**).

The **ReadGMF**() function starting in line 42 expects a file descriptor for an open **G**MF file and calls **parseGMF**() (shown later in Listing 3) to read the file’s **Y**AML content; this returns an array slice of **GitMetaEntry** structures.

# ### Worker Assigned

In line 48 **FindPlugin**() then then checks each array slice element to find the right processor, while the call to **Expand**() in line 52 allows the plugin to discover which actual repositories of the **Cloneable** type the current entry actually points to. The for loop starting in line 56 appends each match to the **Cloneables** instance array, while the exported **AllCloneables**() function in line 63 does no more than return the previous results to the caller as an array slice.

Listing 3 defines which entries are permitted as elements of the long list of entries in the **Y**AML file. An entry can specify a **type**. If this is missing, you are looking at a simple repository definition consisting of the **URL** and its target directory.

The **Go** **GitMetaEntry** type defines all permitted field names of the entries in the **_.gaf** file starting in line 9. In addition to the optional entry **type**, an entry can contain the **URL** and **Dir** fields for a single entry, or the user for a **GitHub** repository (**Figure 3**), or the host and path for an **SSH** host that stores **Git** repositories.

The **parseGMF**() function starting in line 18 expects an open file descriptor, reads **Y**AML data from it, converts the **Y**AML configuration into a list of **GitMetaEntry** objects, and passes these back to the caller.

# ### Simple Plugin

To get started, the plugin in Listing 4 is dedicated to simple entries that contain the **URL** and target directory of a repository to be cloned. Like its big brothers later, it is object-oriented and defines the **NewGMFEntry**() constructor in line 5; the constructor returns a structure that acts as the instance data container, in typical **Go** style. In this simple case, the structure remains un-populated; later, it will be used by the caller as a reference for calling further plugin functions.

The **ApplyTable**() function starting in line 9 checks whether the repository’s **Y**AML definition includes a field named **type**. If this field is missing, it’s a case for the plugin; the function returns **true** because **_e.type == ""** in line 10 evaluates to **true**. Generating and returning a list of structures from the **Y**AML entry in **Expand**(); in this simple case is merely a formality; line 15 adds a single entry to the array slice of **Cloneables**. This concludes our first plugin.

# ### Plugin for GitHub

What about a more advanced plugin, like one that fetches all repos in a user’s **GitHub** account? Listing 5 shows