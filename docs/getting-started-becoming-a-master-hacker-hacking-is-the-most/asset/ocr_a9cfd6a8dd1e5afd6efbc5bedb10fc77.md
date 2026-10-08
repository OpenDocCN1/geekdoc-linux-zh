# **Dictionaries**

Dictionaries hold information as unordered pairs. These pairs contain a key and an associated value. We can use a dictionary to store a list of items and give each item a label so we can refer to it individually.

For instance, we might store the key 1 with the value “Acura,” the key 2 with the value Audi, the value 3 with the value BMW, and so forth. In some systems, these dictionaries might be used to store a USERID (key) with the user password (value). Dictionaries in Python operate like an associative array in many other languages.

Just like the lists we mentioned earlier, dictionaries are iterable. This means that we can use a control structure such a for, if-else, or while to go through each value in the dictionary. This is especially useful for creating password crackers. We could create a script that tries every password in a file until it comes to a correct password or exits.

The syntax for creating a dictionary looks like this; dict = {key1:value1, key2:value2, key3:value3}

Note that with these dictionaries, we use curly braces{} and separate each item with comma. You can include as many key-value pairs as you want.

**Control Statements Control statements allow your script to make decisions based upon some condition such as “as long as this condition evaluates to true, continue. When it evaluates to false, stop.” There are many ways to control the flow of our script in Python. We’ll look at some of the more important ones here.**