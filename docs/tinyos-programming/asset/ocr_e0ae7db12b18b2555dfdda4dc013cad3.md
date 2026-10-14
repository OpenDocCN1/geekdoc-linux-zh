This combine function is bound to error_t with a nesC attribute (attributes are covered in Section 8.4):

```
typedef uint8_t error_t @combine('ecombine');
```

When asked to compile the following configuration

```
configuration InitExample ()
implementation {
  components MainC;
  components AppA, AppB, AppC;

  MainC.SoftwareInit -> AppA;
  MainC.SoftwareInit -> AppB;
  MainC.SoftwareInit -> AppC;
}
```

Listing 4.21 Fan-out on SoftwareInit

the nesC compiler will generate something like the following code:³

```
error_t MainC__SoftwareInit___init() {
  error_t result;
  result = AppA__SoftwareInit___init();
  result = ecombine(result, AppB__SoftwareInit___init());
  result = ecombine(result, AppC__SoftwareInit___init());
  return result;
}
```

Listing 4.22 Resulting code from fan-out on SoftwareInit

Combine functions should be associative and commutative, to ensure that the result of a fan-out call does not depend on the order in which the commands (or event) are executed (in the case of fan-out, this order is picked by the compiler).

Some return values don’t have combine functions, either due to programmer oversight or the semantics of the data type. Examples of the latter include things like data pointers: if both calls return a pointer, say, to a packet, there isn’t a clear way to combine them into a single pointer. If your program has fan-out on a call whose return value can’t be combined, the nesC compiler will issue a warning along the lines of "calls to Receive.receive in CC2420ActiveMessageP are uncombined" or "calls to Receive.receive in CC2420ActiveMessageP fan out, but there is no combine function specified for the return value."

³ The nesC compiler actually compiles to C, which it then passes to a native C compiler. Generally, it uses _ as the delimiter between component, interface, and function names. By not allowing _ in the middle of names, the nesC compiler enforces component encapsulation (there’s no way to call a function with a _ from within nesC and break the component boundaries).