The idea is that the difficulty and an attacker's level of commitment to the attack increase with each additional method. A password can be guessed remotely, but a password with a hardware token is much harder. Now an attacker has to physically interact with the victim, something most common attackers have no interest in. Using all three means that the attacker must have the password, the hardware token, and the biometric all present to authenticate, a fairly daunting proposition for all but the most dedicated attacker.

> TIP
> 
> Some biometric systems use voice prints to identify a user. A person's voice can change over time, be affected by a cold, even by their mood, or by what they had for lunch. As such, to avoid high failure rates, these systems often have their tolerances tuned down, sometimes to the point where a recording of the user's voice will suffice to authenticate with the system. For obvious reasons, in high-security situations, this may be undesirable.
> 
> Any biometric system selected should take into consideration the failure rates and issues associated with a system and their suitability to the expected application.

Proximity cards' main failure is that they are usually a single factor form of authentication, namely the unique identification number. This means that, barring any other methods, an attacker just has to present the unique identifier to the reader to gain access. There is nothing that ties the unique identifier to the person it was issued to and whose access we are impersonating. There is also nothing in this type of system that ties the identifier to the proximity card it is expected to be on.

# Cloning RFID

Since RFID proximity cards are wireless based, this gives an attacker an advantage over something like a physical key. Unlike a physical key that you would need to physically remove from the victim to copy. The wireless nature of the proximity cards means that they can be read at a distance and do not need to be removed.

A large number of proximity card systems in use today, particularly older installations, only use a simple numeric identifier to authenticate. There is no encryption or any verification done on the card, other than to check the number received against a back-end system. This also means that there is no authentication by the card of the reader that is interrogating it. It will respond to any compatible reader and present its numeric identifier to it. This is very useful for an attacker since they can simply wave a reader past a pocket or purse of their victim and the card hands off the identifier. The attacker can then take this information and write his or her own copy of the card to use as they see fit.

In 2003, an engineer by the name of Johnathan Westhues took to tinkering with proximity cards and understanding how they work. Through his efforts, he was able