RC522_GetSector: Reads a 16-byte sector block of data from a card and returns it. You supply the sector number, the authorization key, and the sector number you want to read. This is blocking code in that nothing else can happen until a valid card is read.

RC522_WriteSector: Writes a 16-byte block of data to a sector. You supply the sector number, the authorization key, and the sector number you want to write. This is blocking code in that nothing else can happen until a valid card is presented. It will not, however, allow you to write directly to key sectors.

Let, let's see how this works in practice. Listing 18-1 shows some code to read out the UID of a card.

# LISTING 18-1 Reading the Card's UID

```
#!/usr/bin/python3
# Token reader by Mike Cook
```

```
from rc522rfid import rc522rfid

rfidReader = rc522rfid()

print("Card token reader")
print("Press Ctrl-C to stop.")
while 1: # repeat forever
    cardNumber = rfidReader.RC522_GetCard())
    print(hex(cardNumber))
```

The UID, a 16-bit number, is printed out in hexadecimal format. (Printing in decimal format doesn't make sense, because there will be a mixture of positive and negative numbers, depending on the state of the most significant bit.) So you can now look at the card's number, which is not so exciting, but if you could get that card number to make something happen — like a sound file?

# A simple RFID jukebox

We can use the RFID cards to triggering music from the default Music folder, or from anywhere else, if you like. For example, you can copy over some music loops from the :/usr/share/scratch/Media/Sounds/Music Loops into the /home/pi/Music folder or copy any MP3 files you may