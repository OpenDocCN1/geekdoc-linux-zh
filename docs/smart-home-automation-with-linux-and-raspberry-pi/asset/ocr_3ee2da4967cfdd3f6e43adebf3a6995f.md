This is triggered, indirectly, by cron with several internal timings to cope with the walk between the bedroom and the shower. Instead of writing a direct crontab line such as:

```
10 7 * * 1-5 /usr/local/minerva/bin/routine start 1
```

it is instead better to write:

```
* * * * 1-7 /usr/local/minerva/bin/routine process
```

Because while a lot more processing takes place with it running every minute, it moves control from a (fixed) script in cron, to a more dynamic script in Minerva's configuration directory. This allows you to use variable times in your routine scripts, as these are not supported in cron. For example you could put lights on automatically at sunset, as determined by the utility script sunset.

Structurally, each directory describing the process of a routine includes three files:

```
$ ls /usr/local/minerva/conf/routine/1
name normal script
```

name is a single line text description, which is human-readable and rendered on routine list
normal is the normal time this event should be triggered, for example, 7:00
days lists on which days the even can run, for example, sat,sun. Consequently, you need to create two different routines to handle your weekend wake-up schedule, and your weekday one.
script is the executable to run at that time
There is also one optional file, override, which (if present) uses the time present within it on the following day—and only the following day. The time returns to “normal” for the day after. This is a simple way of introducing the concept of “I need to be up at 6:00 tomorrow, instead of 7:00, for the meeting”, and eliminates a lot of temporary configuration changes.

By having the script and time separate from the cron also allows you to:

+   - Begin with a random sleep delay, to delay events by a few minutes, making the house feel more human.
+   - Look at your current location, with the time-based processor MTS, and disable/enable various events.
+   - Check the weather, and delay your alarm if it’s raining and it knows you’ll be taking the car, instead of waking.
+   - Check the weather, and wake you earlier if it’s snowing, knowing you’ll need more time to defrost the windows.
+   - Check the train times, and delay the alarm if it’s late. Or automatically e-mail your boss if it’s cancelled.
+   - Prevent the event (e.g., starting shower) from happening if it’s detected you’ve already taken a shower.

The use cases may involve starting something sooner, or later, than normal. Because it’s impossible to rewind time, the script should always be triggered on the earliest applicable time for the event, that is, the worse case scenario, and delay the event until the best case. This naturally solves the problem of “dual reality,” where a 6 o’clock alarm might determine that it’s acceptable to wake you at 7 . . . while the 7 o’clock alarm might decide that, due to a change in circumstances, it should rely on the 6 o’clock event to trigger.

Known exceptions to the rule (such as the early meeting example) are still best served with the override file.

As a very developer-centric implementation, this can be easily reprogrammed from the iOS remote application, or tied to the calendar.

And finally, I present a real-world example from my own shower routine! This routine is trigger by my “night time” event, and prepares the shower for me. In addition to basic lighting, it also reads me my schedule for the