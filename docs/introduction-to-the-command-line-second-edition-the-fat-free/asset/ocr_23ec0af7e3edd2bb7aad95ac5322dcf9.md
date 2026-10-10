# ## halt

**Purpose:** Halt the system.

**Usage syntax:** `halt`

```
```
# halt
BROADCAST MESSAGE FROM ROOT: The system is going down for halt now!
* Stopping services                                  [ OK ]
* Terminating processes                                [ OK ]
...
The system will now halt.
```
```

Example output of the halt command

The `halt` command will halt an online system. A halt is a special type of shutdown which gracefully shuts down the operating system without powering off the system.

> > **Note**
> > Some commercial Unix systems will enter maintenance mode when halted. This can be used to access a pre-boot configuration/diagnostic environment.

**Common usage examples:**

+   * `halt` | Halt the system