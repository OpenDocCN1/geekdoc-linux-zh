After your wireless network has been configured, you can use the wireless connections as you would a regular wired Ethernet connection. For example, you can configure TCP/IP on top of your wireless network so that it acts as a gateway to your network's Internet connection. If you are using Linux as a wireless network client as well, you can take full advantage of firewall, masquerading, network proxy, or other networking features to protect and make full use of your wireless network.

# ## Choosing wireless hardware

To get started with a wireless Linux LAN, you need at least two computers and two wireless LAN cards. The wireless LAN cards described in this chapter are PCMCIA-type cards that you insert into those credit-card-sized slots on laptop computers. If ISA or PCI slots alone are available on your computers, you will need to add an adapter card. You may also want (or need) to add indoor or outdoor antennas to your wireless network.

# ### Selecting wireless cards

Not all wireless LAN cards that you can purchase today will work with Linux. When you select a card, make sure that a Linux driver has been created for the card. You will also want to look for several other features:

+   *   **Card type** — Most wireless LAN cards are in PCMCIA (PC-card) form. To use these cards in desktop computers you will probably need an ISA or PCI adapter card.
+   *   **Cost** — If you shop around, you can find wireless LAN cards that cost between $70 and $120 (and the prices will probably have gone down by the time you read this). More expensive cards may include external antennas or better encryption (128-bit as opposed to 64-bit).
+   *   **External connector** — Different wireless LAN cards have different types of connectors, which can lock you into buying antennas from the manufacturer of the LAN card if you are communicating outside of a small area. People who know such things tell me that it is possible to take apart the cards and hack together your own antenna. However, because I don't want to be responsible for wrecking your card, and because there are legal issues related to antenna usage, I don't recommend this.
+   *   **Configurability** — If you really want to fine-tune your wireless LAN, find out how much control you have over configuring a card before you choose it. Descriptions of the *iwconfig* command later in this chapter will help you understand which wireless extensions you can manipulate. Refer to man pages for individual wireless-card drivers (for example, type man *wvlan_cs*), for information on specific parameters that you can change.

I chose to use Orinoco wireless PC cards from Agere Systems to illustrate how to set up a wireless Linux LAN. Although other wireless cards are supported in Linux, Orinoco cards seem to have particularly good Linux drivers, and many people have reported success using them. The cards are also relatively inexpensive (about $70 to $90 at the time of this writing).