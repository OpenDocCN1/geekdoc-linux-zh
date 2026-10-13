
this file in an afternoon and use it for any MIFARE Classic system they encounter. The results of the queries to the reader are looked up, which reveals the key.

Another and even simpler method of recovering the key involves no lookup table at all – it simply uses a weakness in the algorithm to give the attacker the state of part of the algorithm at the end of the transaction (even though it failed) and, with a little computing power, this is enough to determine the key for the system.

Once a key is recovered, the attacker can now use a mobile reader configured with the key to surreptitiously interact with a user's card, and since they authenticate properly, they can read all the information on the card. Once they have that information, they can write it onto another card and it will behave exactly as the cloned user. The Netherlands team demonstrated this with their YouTube video demonstration. In it, the attacker walks up with a laptop to the reader and using the proxmark3, collects a number of authentications and then returns to his accomplices who then use that data to recover the key. They then use the proxmark3 again (this time configured with the key) to wirelessly sniff the contents of a user's card. They then take that information and write it to a whole stack of cards. Each of those cards now authenticates as the cloned user.

> **NOTE**
> The cryptanalysis and internals of the attack could be a book in and of itself and is glossed over here. The original paper describing these attacks is available at http://www.sos.cs.ru.nl/applications/rfid/2008-esarics.pdf

Considering the number of cards deployed and that many secure facilities use this technology, some people were none too happy about this revelation. NXP was certainly not happy. The team planned to present their findings at the Esorics 2008 conference in Istanbul, only to be challenged in court by NXP who filed an injunction to prevent them from presenting their research. The courts eventually found in favor of the researchers and allowed the presentation to proceed.

> **EPIC FAIL**
> This scenario was later brought to the forefront again at the DEFCON 16 conference in 2008. Several students from Massachusetts Institute of Technology (MIT) were scheduled to deliver a talk about the Boston area subway system and several vulnerabilities they have found throughout, from physical to network, social engineering, and ticketing. The Massachusetts Bay Transit Authority (MBTA) took exception to the guerrilla research done to their RFID payment card, named the Charlie card. The students had basically implemented the attack by the Netherlands group and had applied the attack to the MBTA readers. The MBTA filed a last-minute federal lawsuit against the students barring them from delivering the presentation. The Electronic Frontier Foundation (EFF) stepped in and was able to get the lawsuit dismissed, but only after the conference was over, which is what the MBTA seemed to want in the first place.
> The students' slides were posted to the Internet by the MIT student newspaper at http://tech.mit.edu/V128/N30/subway/Defcon_Presentation.pdf. The court documents are available online through the EFF at http://www.eff.org/cases/mbta-v-anderson

## SUMMARY

RFID is a tricky technology to secure. It is wireless, and as such, communications can be read at a distance and captured. Due to their small size, the options for encryption are limited and often rolled by the manufacturer themselves instead of peer-reviewed algorithms, which can lead to them being defeated with ease.

In the end, any system based on RFID should ask the following questions from the beginning: "What do we do if this fails?" "If a tag is cloned, what will the effect be?" "Is there another layer of protection that will minimize the impact if this occurs?" "What is the organizational structure around the use?" "Is it possible to audit its use and monitor for irregularities?" All are tough questions that must be answered.

RFID is a young technology, and developers and society are still adapting to what it all means. There is no simple solution and it is up to the integrator/user of the system to actively think about what the system’s authentication scheme means in a grand sense. Simple authentication with a card may be good at limiting access to the front door of a building from the general public, but perhaps not the crown jewels. RFID-enabled credit cards may seem convenient, but one must weigh the convenience of this against the possibility of a drive by skimming of the credit card details. In that particular case (1 factor), physically swiping the card and requiring a signature is a better (2 factor) and more secure solution to keeping your credit card safe.

## Endnotes

- 1. www.nxp.com/#!/pip/pip=[pfp=41863][pp=[t=epfp,is=41863]
- 2. http://events.ccc.de/congress/2007/Fahrplan/events/2378.en.html

This page intentionally left blank

## Analog Wireless Devices

### INFORMATION IN THIS CHAPTER

- Analog Devices
- Digital versus Analog
- Cordless and Wireless
- Exploiting Analog Wireless
- Scanner Selection
- Wireless Microphones
- Video Devices
- Defense

Many people are amazed by the amount of wireless devices available now. From mouse and keyboards to telephones, everything is being made wireless. It is common for people to interact with wireless devices dozens or hundreds of times a day. We hardly stop to think about it anymore (except when batteries fail). We often fail to assess the security of these everyday items because they are just that, everyday items.

While most modern digital wireless devices offer some level of security in their operation, people often fail to realize that many of the devices they use are still using analog signals to transmit data and offer little to no protection against outside eavesdropping or interference. Even as the first decade of the twenty-first century closes, we continue to use devices using the same technology as over 100 years ago and at just about the same level of security as back then too.

Most offices today have two things on every desk, a computer and a telephone. The computer usually requires two hands, and the phone at least one. Since humans have yet to adapt and grow a third limb, it is easier to adapt the phone. Out of convenience and comfort, most modern offices that spend any amount of time on the phone will often use headsets instead of awkwardly cradling the handset in their shoulder. Modern conveniences have done away with cords and gone wireless, reducing cable tangles and leaving both hands free to work the computer.

Many of these offices, however, never realize that their convenience is potentially bleeding out private, proprietary, or personal information to anyone who cares to listen. A penetration test was able to use these headsets to glean enough information to accurately impersonate a remote employee “visiting” the office. He or she is able to gain full access to the building, bring in accomplices under the guise of vendors, and even be assigned a desk with a handy network connection. He or she spent the next several days scanning the network for vulnerabilities all while consuming the free office coffee, all because of some information gleaned from conversations over wireless headsets.

Often overlooked, analog wireless devices can be a very large gap in the security of any office and must be taken into consideration as part of any security effort.

## ANALOG DEVICES

A well-timed article in January 2008 on the security Web site, DarkReading.com, told a story that many penetration testers are all too familiar with, but it is just a sample of what happens every day and the problem of “we didn’t think about that” security.

The article (http://darkreading.com/shared/printableArticle.jhtml?articleID=208803553) by Steve Stasiukonis explains a scenario he experienced on a penetration test. The client asked his team to test all the radio emissions from the target building, including Wi-Fi, Bluetooth, and anything else the author could find. This was of interest to them as they were keen to try new things and were very interested in the cordless headsets in use by many employees.

They used a handheld radio scanner to scan through common frequencies for these devices and identify headsets in the target office. Once they knew the frequencies, they were able to eavesdrop on phone conversations and glean a large amount of information in a short period of time. Information they gleaned were things like participants in conference calls, employee names, locations, schedules, and other office gossip. It was not just phone calls either. Many headsets continued to transmit after calls were hung up, broadcasting office conversations as well. This information allowed him to impersonate an employee from a remote office visiting the target office. The plan worked frighteningly well. He was able to convince security that he is the employee with some dropped names of employees and a fake business card. He was assigned a desk and given a building access card right away with almost no questions asked. His new desk gave him network access and the freedom to sniff traffic and scan the network all day long.

After a couple of days, he was able to book a conference room and invite a “vendor” (an accomplice actually) in for a meeting. This allowed them more network access and the ability to bring in further attackers past perimeter security. All of this was accomplished with just a little insider knowledge gleaned by listening to insecure transmissions. The amount of information they learned would have allowed them insider knowledge on trade secrets, stock plays, and other very private information.
