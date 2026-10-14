# Table E-1: Escape Commands in mailx (cont.)

| Command | Description |
|---|---|
| -a | Includes the file named `dead.letter`, in your home directory, into the message. The mail variable DEAD may be used to point to a different file. |
| -e | Invokes the editor specified by the EDITOR mail variable to edit the message. |
| -f [msg_list] | Reads the current message or the specified messages into your message. |
| -F[msg_list] | Similar to -f with the difference that all headers will be included regardless of any discard, ignore, or retain commands. |
| -h | Edits the message header fields. This command displays the fields one at a time so you can alter them by adding text to the end, by using the Delete key, or by pressing Ctrl/U to erase the entire field and then retyping it. Use this command with caution. |
| -i string | Inserts the value of the named variable into the mail message.
For example: the command -a is equivalent to the command -i sign to insert your signature into the message. |
| -m[msg_list] | Includes the current message or the specified messages, shifted one tab stop to the right. If the indentprefix mail variable is set, this value is inserted before the tab stop. This is useful to set off messages you are forwarding as part of your new message. |
| -M[msg_list] | Similar to -m with the difference that all headers will be included regardless of any discard, ignore, or retain commands. |
| -p | Displays the message you are composing on your terminal. This is useful to see that the message looks the way you want it to and that it includes the right subject heading and lists of recipients. |
| -q
-q | Aborts the current message as if you pressed two Ctrl/C interrupts. |