![](bbox=[0.12, 0.15, 0.88, 0.4])

# Figure 9.1 Partial component structure of a typical HiiTimerMilliC.

component. Typically (Figure 9.1), it builds up a single timer from hardware counters and interrupts, then virtualizes this single timer into many timers. The virtualizing component, VirtualizeTimerC, stores state for each of the timers it provides, and schedules the single timer it uses to fire when the next provider needs to fire. VirtualizeTimerC is a generic module:

```
generic module VirtualizeTimerC(typedef precision_tag, int max_timers) {
  provides interface Timer<precision_tag> as Timer[uint8_t num];
  uses interface Timer<precision_tag> as TimerFrom;
}
```

# Listing 9.2 VirtualizeTimerC

HiiTimerMilliC must pass the number of timers in the system, obtained using uniqueCount(), to the new VirtualizeTimerC instance:

```
configuration HiiTimerMilliC {
  provides interface Init;
  provides interface Timer<TMilli> as TimerMilli[uint8_t num];
  provides interface LocalTime<TMilli>;
}
implementation {
  enum {
    TIMER_COUNT = uniqueCount(UQ_TIMER_MILLI)
  };
  components new VirtualizeTimerC(TMilli, TIMER_COUNT);
  TimerMilli = VirtualizeTimerC.x
  // More code for wiring VirtualizeTimerC.TimerFrom
}
```

# Listing 9.3 Instantiating VirtualizeTimerC