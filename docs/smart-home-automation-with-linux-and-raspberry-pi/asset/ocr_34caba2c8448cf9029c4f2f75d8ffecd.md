following day. The last point, amusingly, requires additional logic because, if I’m home after midnight, then the “following day” is actually the same day, and we need to amend the process accordingly:

```
# For early morning/late nights
if [ `date +%H` -le 4 ]; then
        REQUEST_DAY=today
        MESSAGE="Back late - I hope it was a good night. Let's talk about the morning"
else
        REQUEST_DAY=tomorrow
        MESSAGE="Let's talk about tomorrow"
fi

CONDUIT=vox
$MINBIN/report $CONDUIT shower echo $MESSAGE

# ... other messages here ...

$MINBIN/report $CONDUIT shower echo Let me look at the calendar
$MINBIN/report $CONDUIT shower calendar $REQUEST_DAY
$MINBIN/report $CONDUIT shower echo Checking house events
$MINBIN/report $CONDUIT shower latest $REQUEST_DAY
$MINBIN/report $CONDUIT shower weather $REQUEST_DAY
```

# Minty

Minty serves two purposes. First, it is a timeout system in which devices will auto-turn off if they are not used within three minutes of their last usage. Second, it is a reference counting utility, to ensure the first component acts intelligently. Therefore, if two people switch the light on, then it switches off three minutes after the last person to switch it off. This is essential in an automated house as it’s possible for one person to switch it on locally, another to do so remotely, and the computer to do it automatically . . . and for all three to expect the device to be on while they’re interacting with it.

To facilitate this, each device has a Minty on event, and a corresponding off event, described in two scripts such as:

```
/usr/local/minerva/conf/minty/shower_speaker/on
/usr/local/minerva/conf/minty/shower_speaker/off
```

So, when the device is first required to switch on, the script minty start shower_speaker is called, and the time is noted. If this is the first time that the shower speaker is being turned on, then the script above is run. If not, its count is incremented. Once you’ve finished using the device, and turn it off (with the predictably named minty end shower_speaker) the count is decremented and, if the count reaches zero, the three-minute timeout begins.

Because the on script is only called on the first invocation, you can trigger the same event from lots of different places. So, for example, the shower speaker remains on if:

+   - you’re playing music in the shower
+   - listening to the computer voice reading your calendar
+   - the shower light is on

Each of these event triggers make an identical call to minty start shower_speaker so only after you have stopped listening to music in the shower, and you’re having your schedule read to you, and you’ve switched the light off, does it get ready to switch it off.

Of course, if you return to the shower within three minutes and play more music, then the three-minute time out begins again.