# The Collections Framework 277

the Comparable interface; when you use a Tree Map, all keys must implement Comparable. In
our example, it's important for prescriptions to be processed in alphabetical order of patient
ID, thenToDoPrescriptions should be a Tree Map. If processing order isn't important, the
Map should be a less-costly Hash Map.

The TreeMap implements the java.util.SortedMap interface, which extends
java.util.Map. The SortedMap interface provides several methods that support
dealing with sorted data.

Object first() Returns this set's first key.

Object lastKey() Returns this set's last key.

SortedMap headMap(Object toKey) Returns a sorted Map containing this Map's mappings
with keys up through the specified key.

SortedMap tailMap(Object fromKey) Returns a sorted Map containing this Map's map-
pings from the specified key through the last key.

SortedMap subMap(Object fromKey, Object toKey) Returns a sorted Map containing
this Map's mappings from fromKey through toKey.

Maps check for uniqueness the way Sets check for element uniqueness; they use
tnequal(), not the == operator. Let's look at an example to see how this works. Recall
t the java.awt.Point contains just an x and y value. Suppose the Map pointTo
associates Strings with Points. How many entries does the Map contain after the following code
executes?

+   1. pointToText.clear();
2. Point p1 = new Point(1, 2);
3. pointToText.put(p1, 'First');
4. Point p2 = new Point(1, 2);
5. pointToText.put(p2, 'Second');

> The Point objects created in lines 2 and 4 are unique but identical. if p1 == p2 is
false, then p1.equals(p2) is true. the put() call on line 5 replaces the single entry that
 added on line 3, and at the end the Map contains only one entry.

# Support Classes

The java.util package contains two support classes, Collections and Arrays These
provide static methods that operate on collections and arrays.

The methods of Collections tend to be advanced, beyond the scope of the Programmer's
Exam. The sample includes one

static boolean disjoint(Collection c1, Collection c2) Returns true if the two
collections have no elements in common.

static int frequency(Collection c, Object ob) Returns the number of elements in
c that are equal to ob.

![](bbox=[0.125, 0.955, 0.833, 0.985])