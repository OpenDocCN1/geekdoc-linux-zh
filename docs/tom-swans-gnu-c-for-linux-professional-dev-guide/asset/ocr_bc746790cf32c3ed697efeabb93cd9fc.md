```
Flo  == 98
Peter  == 78.9
Xavier  == 87.3
```

As in the map.cpp program, scores.cpp declares two typedefs, TScores and TValue, to simplify the creation of a map container and association objects. To create the scores container, the program simply declares it like this:

```
TScores scores;
```

And then, to insert association objects into the container, the program executes statements such as

```
scores.insert( TValue("Barbara", 85.5) );
```

The primary difference between map.cpp and scores.cpp is the way the new program displays association objects. To simplify this process, the program overloads the C++ output stream operator using the following function prototype:

```
ostream& operator<< (ostream& os, const TValue& r);
```

This teaches C++ how to write one association object of the typedef name TValue. The overloaded operator's body writes the object's first and last values using this statement:

```
cout << r.first << "\t== " << r.second;
```

With the overloaded operator, the program can now simply write each association object using an iterator and while loop:

```
TScores::iterator it = scores.begin();
while (it != scores.end()) {
    cout << *it << endl;
    it++;
}
```

Another way to access objects in a map container is to use subscript expressions with key indexes. For example, the following statement displays Peter's score: