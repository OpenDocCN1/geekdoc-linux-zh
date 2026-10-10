# RFID Reader Collision

**RFID reader collision** occurs when the coverage area of one RFID reader overlaps the coverage area of another reader. This collision causes two problems:

+   1.  **Signal interference:** This problem arises when the RF fields of two or more readers overlap and interfere. Programming the readers to read at fractionally different times can help solve this. However, even using this technique some tags may be read twice.
+   2.  **Multiple reads of the same tag:** This problem arises when the same tag is read once by each of the over-lapping readers. To solve this issue, the RFID system must be programmed to read each tag only once in a session.

# RFID Risks

Although RFID technology may enable an organization to increase its efficiency and effectiveness, and support supply chains and other applications using RFID technology, there are some risks involved. RFID technology combines a number of different computing and communications technologies, which makes it complex, and this complexity involves risks. If organizations want to successfully implement RFID technology, they must understand the risks involved and how to manage them. The risks are as follows:

+   -   **Business process risk:** Direct attacks on RFID system components could potentially undermine the business processes the RFID system was designed to enable.
+   -   **Business intelligence risk:** An adversary or competitor could gain unauthorized access to RFID generated information and use it to harm the interests of the organization implementing the RFID system.
+   -   **Privacy risk:** Personal privacy rights or expectations may be compromised if an RFID system uses what is considered personally identifiable information for a purpose other than originally intended or under-stood. The personal possession of functioning tags also is a privacy risk because it could enable tracking of those holding tagged items.
+   -   **Externality risk:** RFID technology could represent a threat to non-RFID networked or collocated systems, assets, and people.

The fact that RF communication is invisible to operators and users increases all of these risks because this makes it more difficult to identify unauthorized behavior.

# Business Process Risk

Organizations often implement RFID systems to replace or enhance a paper-based or partially automated pro-cess. If the RFID system is not properly implemented with business continuity planning, it may be less resilient to disruptions than the original system it replaced. As an example, a warehouse replaces its paper-based inven-tory management system with an RFID-enabled system. The paper system involves storing completed forms at the warehouse and sending the duplicates of the forms to a central office, while the new RFID system locates its back-end database servers at a single computing center. In this environment, the paper system might be more resilient to a local disaster than the RFID system despite the increased efficiency, accuracy, or effectiveness of the RFID-enabled business process.

If any component or subsystem of the RFID system fails, it could result in systemwide failure. In the ware-house example, systemwide failure may occur due to a loss of the network connection between the warehouse and the computing facility, a software virus that disables critical middleware functionality, or a new source of radio interference that prevents readers from accurately reading tags. If an RFID system is unavailable, the business process may slow down, or critical business or operational records may be lost. If the system is mission critical, the consequences could be devastating to the organization's performance.

Human causes, which may be intentional or unintentional, and natural causes both pose business process risks. Cloning is an intentional attack on an RFID business process. In this type of attack, an adversary reads information from a legitimate RFID tag and then programs another tag or device to emulate the behavior of the legitimate tag. Another example of an intentional attack on an RFID business process occurs when, in order to get a better price on an expensive item in a store, a person removes a tag from the item he is intended to identify and attaches it to another item.

Business process risk also involves problems that may occur outside of the RF subsystem. If the network sup-porting the RFID has problems, this will most likely cause problems with the RFID system as well. If a supplier