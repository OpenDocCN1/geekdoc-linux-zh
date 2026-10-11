# ## BASIC BRUTE FORCE ATTACKS

Hashcat uses the “-a3” switch for brute force/mask attacks - You just enter the mask you want to use and it will try every possible character from your specification. Brute forcing is great, but can be very time consuming. An 8 character mask made up all of “?a”, forcing it to try every character, number and symbol for every position, can take an extremely long time to process. You can shorten the time by using the “?u”, “?i”, or “?s” for certain positions. For example, an “-a 3” attack using a mask of “?a?!?u?s” would produce guesses like:

RaiN!
7laB$
*upwJ)

Because of the reduced number of potential characters, you will use, it will crack these much faster than if it had to run through every possible combination of characters.

“?b” takes even longer than “?a”, as it will try every hex character from “00” to “ff”. This includes standard numbers, letters, and symbols, but also extended ASCII characters including foreign and special characters like tab, line feed, etc. But if you need to brute force foreign characters “?b” comes in very handy!