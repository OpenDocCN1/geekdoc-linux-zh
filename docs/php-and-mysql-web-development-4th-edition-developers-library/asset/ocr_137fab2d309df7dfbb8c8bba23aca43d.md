stuff. There’s a place for all that, but I prefer just to say we need to think a bit about what our database will look like: what tables it should contain, what the contents of each table should be, and some of the issues involved in deciding how to represent the data.

The choices made here about data representation are not absolute. In other situations, you might well elect to represent similar data in a different way, depending on the requirements of your applications and the uses to which you intend to put your data.

# ### 1.4.6.1 Tables for the U.S. Historical League

Table layout for the Historical League is pretty straightforward:

+   * A president table. This contains a descriptive record for each U.S. president. We’ll need this for the online quiz on the League Web site (the interactive analog to the printed quiz that appears in the children’s section of the League’s newsletter).
+   * A member table. This is used to maintain current information about each member of the League. It’ll be used for creating printed and online versions of the member directory, sending automated membership renewal reminders, and so forth.

# #### 1.4.6.1.1 The president Table

The president table is simpler, so let’s discuss it first. This table will contain some basic biographical information about each United States president:

+   * Name. Names can be represented in a table several ways. For example, we could have a single column containing the entire name, or separate columns for the first and last name. It’s certainly simpler to use a single column, but that limits you in some ways:
+   
+     * If you enter the names with the first name first, you can’t sort on last name.
+     * If you enter the names with the last name first, you can’t display them with the first name first.
+     * It’s harder to search for names. For example, to search for a particular last name, you must use a pattern and look for names that match the pattern. This is less efficient and slower than looking for an exact last name.

To avoid these limitations, our president table will use separate columns for the first and last names.

The first name column will also hold the middle name or initial. This shouldn’t break any sorting we might do because it’s not likely we’ll want to sort on middle name (or even first name). Name display should work properly, too, because the middle name immediately follows the first name regardless of whether a name is printed in “Bush, George W” or in “George W. Bush” format.

There is another slight complication. One president (Jimmy Carter) has a “Jr.” at the end of his name. Where does that go? Depending on the format in which names are printed, this president’s name is displayed as “James E.