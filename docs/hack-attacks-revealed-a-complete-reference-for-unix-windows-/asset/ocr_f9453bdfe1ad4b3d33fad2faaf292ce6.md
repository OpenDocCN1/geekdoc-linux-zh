![](bbox=[0.11, 0.05, 0.5, 0.065])

To help understand Token Ring networking, imagine a series of point-to-point stations forming a circle (see Figure 3.7). Each station repeats, and properly amplifies, the signal as it passes by, ultimately to the destination station. A device called a Multistation Access Unit (MAU) connects stations. Each MAU is connected to form a circular ring. Token Ring cabling may consist of coax, twisted pair, or fiber optic types.

![](bbox=[0.12, 0.22, 0.55, 0.68])

# Operation

Token Ring functionality starts with a 24-bit token that is passed from station to station, circulating continuously, even when no frames are ready for transmission. When a station is ready to transmit a frame, it waits for the token. Upon interfacing the token, the station submits the frame with the destination address. The token is then passed from station to station until it reaches the destination, where the receiving station retains a copy of the frame for processing. Each connection may retain the token for a maximum period of time.

This may seem arduous, but consider that the propapagation velocity in twisted pair is .59 times the speed of light. Also, because each station must wait for the passing token to submit a frame, collisions do not occur in Token Ring.

# Token Ring Design, Cabling