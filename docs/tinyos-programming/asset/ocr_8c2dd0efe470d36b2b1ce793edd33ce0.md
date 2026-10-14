The former has the problem of code duplication (and file bloat), while the latter depends on run-time checking, which is notably deficient in C. Having a generic queue enables compile-time checking for the values put in and out of a queue.

# 3.2.2  Bidirectional interfaces

So far, we’ve only seen interfaces that have either commands or events, but not both. Bidirectional interfaces declare both commands from a user to a provider as well as events from a provider to a user. For example, this is the Notify interface, which allows a user to ask that it be notified of events, which can have data associated with them:

```
interface Notify<val_t> {
  command error_t enable();
  command error_t disable();
  event void notify(val_t val);
}
```

Listing 3.12  The Notify interface

The Notify interface has two commands, for enabling and disabling notifications. If notifications are enabled, then the provider of the interface signals notify events. The Notify interface is generic as, depending on the service, it might need to provide different kinds of data. Bidirectional interfaces enable components to register callbacks without needing function pointers.

For instance, some hardware platforms have a button on them. A button lends itself well to the Notify interface: a component can turn notifications of button pushes on and off. For example, UserButtonC is a component that provides this abstraction:

```
configuration UserButtonC {
  provides interface Get<button_state_t>;
  provides interface Notify<button_state_t>;
}
```

Listing 3.13  UserButtonC

![](bbox=[0.184, 0.805, 0.493, 0.916])

**Figure 3.4**  Commands and events for UserButtonC.