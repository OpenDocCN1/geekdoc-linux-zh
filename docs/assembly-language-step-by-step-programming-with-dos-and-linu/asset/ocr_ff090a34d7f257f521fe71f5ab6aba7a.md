door is number 1, and so on. You don't have to knock on the door of bit 0 and ask which bit it is, go to the next door and ask there too, until you find the bit you want. If you have the address, you can zip right down the street and park square in front of the bit you intend to visit.

Each chip has a number of pins coming out of it. (This is the computer room's equivalent of the Killer Rake: Don't step on one in the dark!) The bulk of these pins are called address pins. One pin is called a data pin. (See Figure 3.2.) The address pins are electrical leads that carry a binary code. Your address is a binary number, expressed in 1s and 0s only. You apply this address to the address pins by encoding a binary 1 as (say) 5 volts, and a binary 0 as 0 volts. Special circuits inside the RAM chip decode this address to one of the select inputs of the numerous memory cells inside the chip. For any given address applied to the address pins, only one select input will be raised to five volts, thereby selecting that cell.

![](bbox=[0.189, 0.477, 0.535, 0.908])

Figure 3.2 A RAM chip.