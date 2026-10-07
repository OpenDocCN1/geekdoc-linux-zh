# Chapter 6 · Objects and Classes

There is only one disadvantage to the typeface enumeration pattern: it requires a lot of coding. The LightState class shown above is easy enough to create, a large program with lots of formalized states might require dozens of enumeration classes, and even seasoned developers might be tempted to cut corners.

Java 5.0's typeface enumeration support provides all the benefits of the LightState class with very little programming effort. The similarities between traditional classes and enums include the following:

+   * You can declare an enum anywhere you can declare a class.

+   * Compiling an enum generates a .class file name which is derived from the enum's name.

+   * Enums inherit data and methods from Object.

+   * Enums may be converted and cast to the same rules that govern any class that extends Object.

+   * Enums may have main( ) methods and can be invoked as applications.

+   * Enums have no explicit constructors get default no-args constructors.

Enums have restricted functionality. They are unlike traditional classes in the following ways:

+   * Enums are declared with the enum keyword rather than the class keyword.

+   * Enums may not extend anything and may be extended.

+   * Enums may be arguments in switch statements.

+   * Enums have built-in name( ) and toString() methods, both of which return the name of the current instance.

The first statement of an enum has a special format, as shown below. Here is LightState rewritten as an enum:

```
public enum LightState {
  RED, YELLOW, GREEN;
}
```

Notice the first (and only statement, which is the comma-separated list of identifiers, terminated by a semicolon. When an enum is class-loaded, one instance is created for each identifier in the list; you can think of the identifiers as the names of the instances. The names become public static final members of the enum, so you can refer to the instances as, for example, LightState.YELLOW. The instances are called the enum constants.

The code that follows shows how to use the LightState enum. Assume the getState() method returns a LightState rather than an int:

```
switch (nextTrafficLight.getState()) {
  case LightState.RED:
    stop();
    break;
```