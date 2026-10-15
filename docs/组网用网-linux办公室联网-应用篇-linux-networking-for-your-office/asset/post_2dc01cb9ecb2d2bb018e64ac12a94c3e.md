
## CAUTION

Prior to the acceptance of v.90 as a standard for modem communication, two competing and proprietary protocols were in use, X2 and K56Flex. You’re unlikely to find modems that use only these protocols in stores today, but you might find one in the used market. Such models can often be upgraded to use v.90, but a few, particularly from now-defunct manufacturers, may not be upgradeable. Some ISPs may still support one or both of these older protocols, but sooner or later this support is likely to vanish, after which such modems will effectively be 33.6Kbps models.

Telephone modem speeds aren’t likely to increase substantially, if at all, in the future. v.90 is more or less at the theoretical limit for data transmission rates over conventional telephone lines when using modem technology. It is possible to coax more speed out of telephone wires, but only by switching to digital technologies such as DSL.

## Testing for v.90 Compatibility

Although most phone lines in the United States are capable of handling v.90, not all are. You can test your current phone line by using the line test service operated by 3COM, assuming you have a v.34 (28.8Kbps or better) modem. You’ll need to launch a terminal program such as Minicom or Seyon and configure it to use your modem line (generally /dev/ttyS0 or /dev/ttyS1). Type ATDT1-847-262-6000 to have the modem dial this line test number. (Note: This is a toll call!) When you’re prompted for your first and last names, enter line and test, respectively. The system will then diagnose the connection and inform you of the results.

When testing for 56Kbps capability, you should be sure to test from the line you intend to use for the modem connection. It’s possible that two phone lines on a street, or even in a building, will have different characteristics, so you shouldn’t rely on your neighbor’s ability to connect at high speeds; test your own line.

Although generally accurate, the results of the 3COM test aren’t perfect. In some cases, you may find that your line tests well for 56Kbps speed, but when you connect an appropriate modem, you only get speeds of around 40Kbps—hardly worth the upgrade from 33.6Kbps. It’s conceivable that you could improve matters by removing unneeded telephones from your home wiring or by having the phone company look at your wires, but you may be stuck with it. The v.90 standard pushes the analog telephone system about as far as it can go, and any minor imperfection can cause a substantial drop in performance.

## Linux Modem Compatibility

Most modems operate over a conventional serial port (usually /dev/ttyS0 or /dev/ttyS1 in Linux). As such, they don’t need special drivers beyond the normal Linux serial drivers. There are some caveats, however, as well as reasons for preferring one type of modem over another.

In addition to their serial port interfaces, modems use command sets to perform actions such as dialing, setting error correction, and so on. The basics of this command set have long been standardized as the Hayes command set, named after the modem manufacturer that developed it. The Hayes command set is quite basic, however, and different manufacturers have extended it in various ways. None of these extensions is incompatible with Linux, however. At worst, you’ll need to change the modem initialization string you use in your GUI PPP dialer or PPP dial scripts to enable or disable certain features.

## External and Internal Modems

You can purchase modems that come as boxes external to the computer and that plug into the computer’s external serial port, or as internal cards that plug into an ISA slot (or more recently, a PCI slot). Traditionally, internal modems have contained serial port circuitry, and so appear to Linux as a serial port. The main trick with internal modems of this type is that you may need to configure them as a third serial port (/dev/ttyS2) with its own separate IRQ, or disable one of the serial ports on the motherboard and have the internal modem take its place. Both of these options can be troublesome, and so internal modems tend to be trickier to configure for Linux than external models. External models also have the advantage of indicator lights that can help in diagnosing link problems. On the other hand, external models take up desk space and require a separate power supply. Overall, I tend to favor external models, but this is a matter of personal preference.

## A Word About Windows-Only Modems

In the past few years, internal modems have begun to appear that don’t use a standard serial interface and offload much of a modem’s traditional functionality onto the computer. Such modems often emulate the serial port using special Windows drivers. In theory, Linux drivers could be developed for such Windows-only modems, but Linux developers have spurned the challenge for a variety of reasons, including the facts that such modems degrade overall system performance and that modem manufacturers haven’t been forthcoming with the specifications needed to develop drivers. Needless to say, you should avoid Windows-only modems for use in Linux.

## NOTE

> One company, PCtel (http://www.pctel.com), has announced a software-driven modem for Linux similar in concept to Windows-only modems.
