# Enums 197

A more robust approach is shown here:

```
public class LightState {
    protected final String name;

    public final static LightState RED = new LightState("red");
    public final static LightState YELLOW = new LightState("yellow");
    public final static LightState GREEN = new LightState("green");

    private LightState(String s) {
        name = s;
    }

    public String name() {
        return name;
    }
}
```

The new approach represents states by using instances of the LightState class, rather than ints. Note that the constructor is private, so you can never construct any instances from outside the class or its subclasses; the only instances you will ever need are constructed statically. You can't use the new class as a switch statement argument as you could with the ints of the previous example, but that's a small price to pay. Our original switching becomes

```
LightState state = nextTrafficLight.getState();
if (state == LightState.RED)
    stop();
else if (state == LightState.YELLOW)
    floorIt();
else if (state == LightState.GREEN)
    proceed();
else
    assert false : "null light state";
```

This design ensures that the only unexpected state value for a traffic light is null. Also, debugging code can print any LightState instance and produce an informative result. In fact, this approach is so useful that it has a name: the enumeration design pattern. It is considered typesafe because there is a dedicated type whose sole purpose is to encode a few enumerated states, avoiding the dangers of using assigned ints (Arbitrarily assigned ints or other primitives knows as enumerated constants.) Some programming languages (Pascal, for example) have built-in support for typesafe enumerations. Java did not, until 1.5.