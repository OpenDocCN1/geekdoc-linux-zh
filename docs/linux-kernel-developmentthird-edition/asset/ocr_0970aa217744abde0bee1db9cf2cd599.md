softirqs, `__do_softirq()` loops over each one, invoking its handler. Let’s look at a simplified variant of the important part of `__do_softirq()`:

```
```
u32 pending;

pending = local_softirq_pending();
if (pending) {
  struct softirq_action *h;

  /* reset the pending bitmask */
  set_local_softirq_pending(0);

  h = softirq_vec;
  do {
    if (pending & 1)
      h->action(h);
    h++;
    pending >>= 1;
  } while (pending);
}
```
```

This snippet is the heart of softirq processing. It checks for, and executes, any pending softirqs. Specifically

+   1. It sets the **pending** local variable to the value returned by the `local_softirq_pending()` macro. This is a 32-bit mask of pending softirqs—if bit n is set, the nth softirq is pending.
+   2. Now that the pending bitmask of softirqs is saved, it clears the actual bitmask.
+   3. The pointer h is set to the first entry in the **softirq_vec**.
+   4. If the first bit in **pending** is set, h->action(h) is called.
+   5. The pointer h is incremented by one so that it now points to the second entry in the **softirq_vec** array.
+   6. The bitmask **pending** is right-shifted by one. This tosses the first bit away and moves all other bits one place to the right. Consequently, the second bit is now the first (and so on).
+   7. The pointer h now points to the second entry in the array, and the **pending** bitmask now has the second bit as the first. Repeat the previous steps.

∗ This actually occurs with local interrupts disabled, but that is omitted in this simplified example. If interrupts were not disabled, a softirq could have been raised (and thus be pending) in the intervening time between saving the mask and clearing it. This would result in incorrectly clearing a pending bit.