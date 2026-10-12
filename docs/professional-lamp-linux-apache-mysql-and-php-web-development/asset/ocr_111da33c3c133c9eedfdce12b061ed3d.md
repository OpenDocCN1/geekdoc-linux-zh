# Chapter 2

```
`<?php

class Shape
{
public function draw()
{
echo 'Shape::draw() has been called.\n';
}
}

class Circle extends Shape
{
public function draw()
{
echo 'Circle::draw() has been called.\n';
parent::draw();
}
}

$c = new Circle();
$c->draw();
?>`
```

This would show the following when run:

```
`Circle::draw() has been called.
Shape::draw() has been called.`
```

In this example, you’ve defined a subclass `Circle` that extends from the base class, `Shape`. Since you created a new `draw()` method in the subclass, you use `parent::draw()` to call the same-named function in the parent class. Calling a parent method in this way is a common practice when overriding a base method in a subclass, and is quite frequently used in constructors to call the parent constructor—the base class’s constructor is not automatically called otherwise.

# ### Abstract Classes

You may find during programming or design that you have classes like `Shape` that need to be created to give subclasses identical properties or methods, but never need to be instantiated on their own. The `Shape` class you used earlier would be a perfect candidate for becoming an abstract class—you’ll never want to create a `Shape` object directly, but it’s necessary for provided functionality to more concrete subclasses of geometric objects. For this type of scenario, there is the `abstract` keyword.

When a class is defined as `abstract`, other classes can extend it, but it cannot itself be instantiated. For example:

```
`<?php
abstract class Shape
{
public $origin = array('x'=>0, 'y'=>0);`
```