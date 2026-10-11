After you build the pattern, you need to assign the action, which can be any one of the items outlined in Table 9.4. When an action has a value associated with it, you use the format *action=value*.

Finally, you can specify how often the pattern has to match before it becomes a concern. This is optional; you do not have to include it in any /etc/swatchrc rule. If you do, however, use one of the formats listed in Table 9.5.

# Attacks And Intrusions

The number of ways for people to attack your network or machines, or just sneak their way in, is ever growing. The only way to keep up on these techniques is to read the security sites previously listed in “Online Security Resources.” However,

**Table 9.4 Actions available in the swatch tool.**

| Action | Result | Values | Default |
|---|---|---|---|
| **bell** | Sounds a speaker bell and echos the contents of the line that matches the pattern | A nonzero positive integer, reflecting the number of bells | 1 |
| **echo** | Echoes the line that matches the pattern | Formatting for the line, out of the following options: **blink**, **bold**, **inverse normal**, or **underscore** | Normal |
| **exec** | Commands to execute if pattern matches | Path to command | None |
| **ignore** | Ignores the line that matches this pattern | None | None |
| **mail** | Sends mail if the pattern matches | *address1:address2…* | User running the program |
| **pipe** | Sends the matched line through a pipe to a command | Path to command | None |
| **write** | Echoes the matched pattern to the listed users with the **write** command | *login1:login2…* | None |

**Table 9.5 Time intervals between matches in /etc/swatchrc.**

| Format | Units |
|---|---|
| ## | Seconds |
| ##:## | Minutes:seconds |
| ##:##:## | Hours:minutes:seconds |