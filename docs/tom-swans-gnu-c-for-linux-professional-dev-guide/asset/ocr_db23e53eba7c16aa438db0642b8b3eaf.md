actually counts the number of values in aList that are less than or equal to 8 (or, more strictly speaking, the number of values for which 8 is greater). To make the statement count the number of values greater than 8, replace the count_if() statement with the following:
count_if(aList.begin(), aList.end(),
bind2nd(greater<int>(), 8), k);
cout << "Number elements > 8 = " << k << endl;

This code is written as a comment at the end of the listing file. Because bind2nd() is now used, the resulting function object performs the expression:
q > 8
where q is again a value from the container. Thus, the modified statement counts the number of elements greater than 8.

# NEGATOR FUNCTION OBJECTS

A negator creates a function object from another function object, but it has the opposite effect. Where the original function returns true, the negator object returns false. There are two negators in the STL (Standard Template Library): not1() and not2(). Pass any unary function object to not1(). Pass any binary function object to not2(). Negators are often used in conjunction with binders to create function objects with a negated logic.

For example, you might use a negator to search a list of values. Using a copy of the program binder.cpp (refer to Listing 23.11), construct an iterator named start for the list<int> class and assign to the iterator the result of the find_if() algorithm. The following code demonstrates this process by searching the list for a matching condition:

```
list<int>::iterator start;
start = find_if(aList.begin(), aList.end(),
bind2nd(greater<int>(), 6));
if (start != aList.end())
cout << "start == " << *start << endl;
```

The condition for the search is specified by the binder bind2nd(). After the search, if start is not equal to the past-the-end value, the iterator addresses the first listed value greater than 6. To perform the opposite search and look for the first value that is not greater than 6, pass the binder expression to not1() as follows:
start = find_if(aList.begin(), aList.end(),
not1(bind2nd(greater<int>(), 6)));

You must use not1() in this case because bind2nd() returns a unary_function object. Use not2() similarly to create a function object for any binary_function object.