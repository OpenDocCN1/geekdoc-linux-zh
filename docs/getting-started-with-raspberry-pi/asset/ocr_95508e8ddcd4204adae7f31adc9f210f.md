# The 1-Wire Bus

The $1$-wire protocol developed by Dallas/Maxim uses a 1-wire (or $w1$) bus that carries both power and signal; the return ground path is provided using some other means. It provides a simple way to interface with slow devices by reducing space, cost, and complexity. An example device that works using this protocol is the $i button$ (www.ibutton.com), which is used for sensing temperature, carrying data, or holding unique IDs.

Another $w1$ chip that interfaces through a single port pin of an embedded controller is the DS2433 4kb 1-wire EEPROM from Dallas/Maxim. The driver for this chip, $drivers/w1/slaves/w1\_ds2433.c$, exports access to the EEPROM via a sysfs node.

The main data structures associated with a $w1$ device driver are $w1\_family$ and $w1\_family\_ops$, both defined in $w1\_family.h$.