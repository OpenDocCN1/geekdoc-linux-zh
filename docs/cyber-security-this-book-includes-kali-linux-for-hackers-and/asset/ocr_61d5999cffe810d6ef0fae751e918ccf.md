# Cryptography Used to Maintain Communications Security

There are two types of protection available depending on the level of communication that you would like to use. First, link encryption repeatedly encrypts and decrypts all information sent as part of data transmission while end-to-end encryption only encrypts the internal information sent but not the packet header information that is necessary for routing.

# Link Encryption

As mentioned earlier, all data is encrypted in this type of data transmission with the exception of the data-link control information. As it moves along its route to the destination host, each router at a certain point decrypts the information in order to obtain header information for its destination and encrypts the information again.

As a person sending data over the internet, either by email or in which banking institutions have to communicate with their customers, then link encryption is preferred. This is because all data is encrypted and provides privacy and security. On the downside, all devices the data passes through must receive the key and key changes if necessary. Apart from this, the decryption of the packet at each routing point has to take place in order for it to move further along the route.

# End-to-End Encryption

In this type of encryption, encryption of the data is restricted to everything apart from packet headers and addresses. This makes it more susceptible to hackers who can gain more information about packets by sniffing or eavesdropping. Still, end-to-end encryption allows for users to have control over what gets encrypted or not. In addition, since there is no repeated decryption or encryption at each routing point, the performance of routing devices improves greatly. IPSEC is one such example of end-to-end encryption.

# Actively Secure Network Components