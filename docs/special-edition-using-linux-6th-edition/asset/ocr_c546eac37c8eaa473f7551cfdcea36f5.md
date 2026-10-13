**TABLE 20.1 HOSTS ON TWO SAMPLE LANS**

| LAN Site 1 | LAN Site 2 |
|---|---|
| California: (192.168.1.1)<br>(Internet connection: 123.123.123.1) | New York: (192.168.2.1)<br>(Internet connection: 200.200.200.1) |
| Encino (192.168.1.2) | Albany (192.168.2.2) |
| SantaB (192.168.1.3) | Erie (192.168.2.3) |
| SanF (192.168.1.4) | NYC (192.168.2.4) |
| LAX (192.168.1.5) | Buffalo (192.168.2.5) |
| Bakersfield (192.168.1.6) | Rochester 192.168.2.6) |

If you set up California and New York as encrypted gateways, all traffic behind the gateways will be encrypted when communicating from California to New York. So all traffic from SantaB to NYC will be encrypted before leaving California and decrypted before leaving New York. However, traffic between hosts Encino and LAX, for example, will not be encrypted. Likewise, traffic that originates on California and goes to any other host (including New York or any host behind it) will not be encrypted.

So any host behind California will be able to read any traffic originating or terminating (or both) with any other host behind California. The same holds true for hosts behind New York. And traffic originating on either gateway is sent unencrypted.

If SanF and Albany belong to the president and vice president of the company and they need to set up private communications that no other host will be able to read, including on their own subnet, they will need individual host setups that also build an encrypted tunnel directly between SanF and Albany. If the gateway tunnels are active, the encrypted tunnel between SanF and Albany will travel through it. There is no problem having an encrypted tunnel through another encrypted tunnel apart from the slight lag each end might notice because of the dual encryption (depending on the speed of the systems encrypting/decrypting). The same concept applies if NYC needs to communicate with Albany securely. These two will need to set up individual tunnels between each other.

# VPN CONFIGURATION

The ipsec configuration files consist of two separate files. The first is `/etc/ipsec.secrets`. Within the `ipsec.secrets` file is either a pre-shared secret key (PSK) or an RSA key (RSA). This text will deal only with the preshared secret. This shared secret will be identical between two systems and allows these two systems to authenticate each other through this shared secret. This method is secure as long as the shared secret remains secret.

> **Caution**
> 
> The shared secret in `ipsec.secrets` must never be transmitted in the clear. Maintain the secret by ensuring that only root can read the file (chmod 600), and transfer the secret to the other system only by a secure means (put the `ipsec.secrets` file on a floppy and use the sneaker net—hand carry it—or transfer it through openssh, or secure shell).