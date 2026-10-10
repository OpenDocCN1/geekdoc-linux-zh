The **el if** statement enables you to nest tests one after another within an overarching **if** statement. If all of those tests fail, you may want to provide some fallback code. This code is specified by starting a block with the **else** statement. Commands after **else** but before **fi** execute only if the **if** statement and any intervening **el if** statements evaluate to false.

To illustrate **if**, **el if**, and **else** in action, consider Listing 31-9. This script attempts to identify the chipset used by an Ethernet card based on its assigned device name, as reported by **ifconfig**. To do so, this script first isolates the names of all the Ethernet cards, using **ifconfig**, **grep**, and **cut**, much as Listing 31-3 does. The resulting **$iface** value, however, includes *all* the interfaces, so another use of **echo** and **cut** isolates just the first of these interface names. **$iface** then contains a string that can be compared using **if** operators. In this particular case, the order of the comparisons is unimportant. The main **if** statement compares **$iface** to the string **fxp0**, which identifies Intel EtherExpress Pro 100B boards. If a match is obtained, the script prints this information and skips the rest of the comparisons. If a match isn't found, the script goes on to the next comparison, which identifies DEC/Intel Tulip chipsets via an **el if** statement. The second **el if** identifies boards that use VIA Rhine chipsets. If none of these comparisons matches, the script uses the **else** clause to give up, notify the user of that fact, and tell the user what the device name is.

+   **Listing 31-9 A Script Demonstrating the Use of if, el if, and else**

```
#!/bin/sh

# Get all interface names
iface=`ifconfig | grep flags | cut -f 1 -d " ":`"

# Isolate the first interface (normally the first Ethernet device)
iface=`echo $iface | cut -f 1 -d " "`

# Identify the hardware
if [ $iface = "fxp0" ]
then
	echo "This computer has an Intel EtherExpress board."
elif [ $iface = "de0" ]
then
	echo "This computer has a DEC/Intel Tulip chipset."
elif [ $iface = "vr0" ]
then
	echo "This computer has a VIA Rhine chipset."
else
	echo "I can't identify this computer's primary network card."
	echo "The unidentified interface name is" $iface
fi
exit 0
```