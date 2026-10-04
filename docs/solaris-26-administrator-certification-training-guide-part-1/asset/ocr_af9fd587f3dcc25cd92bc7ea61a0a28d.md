+   2. Check for the following line in the /etc/remote file. If it is not there, add it after the hardware:\ entry. For the ttyb port, add the following lines:
```
hardware:\ :dv=/dev/term/b:br#9600:e1="C'S'Q'U'D:ie=%$ioe=D:
modem1:\ :dv=/dev/cua/b:br#9600:
```
Make sure the baud rate matches the baud rate you selected when setting up the serial port.

3. Check the permissions and owner of the modem port. The file /dev/cua/b should be rw-rw-rw- and the owner should be uucp. If not, use the chmod command to change the permission and the chown command to change the owner.

4. After modifying the /etc/remote file and checking the permission of the port, issue the following command:
```
tip modem1
```
You should get a "connected" message. If you get anything else—for example, "all ports busy"—check the /etc/remote device entry as described in step 2.

5. Verify that the modem is responding to commands. Do so by typing
```
at <cr>
```
You should see an OK displayed.

6. Check the modem register and initialization string. Refer to Table 12-9 for common modem initialization strings and see if the modem type is referenced. If so, follow the manufacturer's instructions for using that string to initialize the modem. For example, the US Robotic Courier Modem string is
```
AT&F1&B1&C1&D2X50=18W
```
If you do not know the initialization string, refer to the manuals supplied with your modem. If you still cannot figure out the initialization string, contact the modem manufacturer's technical support.

7. After setting up the modem, exit the "tip" utility by typing the following sequence:
```
<cr>~.
```
The above sequence is a "carriage return" followed by a "~" character and a "." character.