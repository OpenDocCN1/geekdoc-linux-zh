# Chapter 6 · Objects and Classes

bug related to storing your class in a collection, check your equals() and hashCode() methods to make sure they obey their contracts.

The hash code contract specifies behavior of the hashCode() method. A hash code is an int that represents the uniqueness of an object; it is used by classes that need an efficient way to determine whether two objects contain different values. The contract is specified on the API page for java.lang.Object, in the hashCode() method description. It requires that if two objects are equal according to their equals() methods, then they must have equal hash codes. Note that the converse is not part of the contract; it's okay for unequal objects to have the same hash code.

Consider a class Point3D, representing a point in three-dimensional space. A reasonable implementation would do

```
public class Point3D {
    private int x, y, z;

    public boolean equals(Object ob) {
        Point3D that = (Point3D ob);
        return this.x == that.x &&
               this.y == that.y &&
               this.z == that.z;
    }

    public int hashCode() {
        return x + y + z;
    }
```

Two instances of this class are equal if their x, y, and z values match. Clearly the hash code contract is honored. Note that it is possible for unequal instances to have equal hash codes. For example, one instance might have values (100, 200, 300) while another has values (600, 1, -1). This is acceptable. However, be aware that collection classes may slow down when dealing with unequal objects with equal hash codes.

A hash code algorithm would strike a reasonable balance between detecting uniqueness and running efficiently. You can avoid slow collisions by writing hashCode() methods that are scrupulous about uniqueness, but it does no good to speed up collection efficiency if your scrupulous hashCode() methods are inefficient. For example, you might wonder if the following alternative hashCode() version for Point3D:

```
public int hashCode() {
    return (int)(Math.pow(2, x) +
                 Math.pow(3, y) +
                 Math.pow(5, z));
}
```