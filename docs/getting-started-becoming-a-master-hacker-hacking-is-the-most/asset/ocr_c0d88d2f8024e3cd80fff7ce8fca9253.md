task. To remedy this situation, the industry developed a technology to make setting up a Wi-Fi AP as easy as pushing a button! What could possibly go wrong?

The new technology became known as Wi-Fi Protected Setup or WPS. It enabled the user to setup their Wi-Fi access point by simply pressing abutton on the AP. This system relies upon a PIN being transmitted between the AP and the client to initiate their “secure” connection.

This PIN uses only digits from 0-9 (no special or alphabetic characters). The PIN is eight characters long (all characters are digits), and the eighth character is a checksum. To make matters worse, of these seven remaining characters, the first four are checked, and the last three are checked separately. This means that the number of possibilities is 104 (10,000) + 103 (1000) = 11,000 possible PIN’s! With that small number of PIN’s our computer can test each of them in a matter of hours.

Although this vulnerability was mitigated with the development of WPS 2.0 in 2012, there are still a number of APs with WPS 1.0 and vulerable to this attack (I estimate about 10-20 percent) The crack the WPS PIN, you will need the following information; 1. The name of your interface (usually wlan0mon) 2. The MAC Address of the AP

# 3. The ESSID of the AP

+   4. The channel that the AP is broadcasting on We can gather all that information from our airodump-ng screen.