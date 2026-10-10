This example is a simplified version of the ActionScript code that is generated. In the above code snippet, in (1), the `import` tells the compiler that the application needs the mentioned classes ready for use in the future.

In (2), a button is declared, `compute`. It is similar to the `id` attribute in MXML. This can be used to refer this button later in your code.

In (3), an instance of the button `compute` is created. This is done by using `new` keyword. It is followed by the constructor of the object that initiates the object creation.

In (4), the attribute `label` is assigned a value using the dot notation. This signifies that `label` is a property of `Button` class.

In (5), the mapping between MXML attributes for styles to ActionScript can be seen.

The method `setStyle()` takes two parameter and is used to set a style for a component. The first is the name of the style, in this case `borderColor` and the second is the value for that style.

The method `getStyle()` takes a single parameter and returns the value set for the style sent as parameter to the method for a component.

# 3.3.8 Events

An `event` is a runtime occurrence that has a potential to trigger a response in a program. In ActionScript, there are two kinds of events: `built-in events` and `custom events`. `Built-in events` describe changes to state of the runtime environment like the clicking of a mouse and `custom events` describes changes to the state of program like the end of program.

> **Note:**
> 
> ActionScript event architecture is based upon the W3C DOM (Document Object Model) Level 3 Event Specification.

For event handling in ActionScript, `event listeners` are used. An event listener is a function that executes when a given event occurs. It listens continuously for a given event to occur. To notify the program when an event occurs, ActionScript executes all the event listeners that are registered to execute for that event. This notification process is called the `event dispatch`. The piece of code that executes when an event occurs is called the `event handler`.

# 3.3.8.1 Event Object

When an event occurs in ActionScript, an `event object` is created. Every event has two properties, `target` and `type`. The target property specifies the target object which caused the event and the type property specifies the type of event, for example, a click, a mouse move, etc.