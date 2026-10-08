**Wireless Cryptography** Wireless cryptography has been a favorite as so many are [trying to crack wireless access points](#). As you might guess, wireless cryptography is symmetric (for speed), and as with all symmetric cryptography, key exchange is critical.

+   - 	

**WEP** - This was the original encryption scheme for wireless and was quickly discovered to be flawed. It used RC4, but because of the small key size (24-bit), it repeated the IV about every 5,000 packets enabling easy cracking on a busy network using statistical attacks.

325 | Page

+   - 	

**WPA** - This was a quick fix for the flaws of WEP, adding a larger key and TKIP to make it slightly more difficult to crack.

+   - 	

[**WPA2-PSK**](#) - This was the first of the more secure wireless encryption schemes. It uses a pre-shared key (PSK) and AES. It then salts the hashes with the AP name or SSID. The hash is exchanged at authentication in a four-way handshake between the client and AP.

+   - 	

**WPA2-Enterprise** - This wireless encryption is the most secure. It uses a 128-bit key, AES, and a remote authentication server (RADIUS).

326 | Page