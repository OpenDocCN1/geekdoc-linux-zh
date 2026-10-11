```
65.66.67.10 65.55.76.11 : PSK '0x6c75ff4e_726ffd6f_08e0d143_3d31cd8e\_ 1279a10c_44f0eb1c_0398b736__c50647f2'
# RSA private key
10.0.0.1 10.0.0.2: RSA {
    Modulus: xcce0dfafeb7b00d6d8ac7988f1831e...
    PublicExponent: 0x03
    PrivateExponent: x889d5ea7547a7aabe6f657698...
    Prime1: xe8fa28491068933b4b58920ffde71fdb a...
    Prime2: xe12c294a7d3cfa110cacc332073e95166...
    Exponent1: x9b517030b59b0cd232b0acaa944bf...
    Exponent2: x961d70dc537dfc0b5dc87776af7f0e...
    Coefficient: x261e965745e79966d4216ce281c7...
}
```

> NOTE   In the preceding example, the lines ending in ... have been concatenated for brevity.

The format of an entry in the /etc/ipsec.secrets file is
`index1 index2 ... index-n : [PSK|RSA] 'secret-key'`
where *index1*, *index2*, and so on, can be one of the following constructs:

+   - A numeric IP address (e.g., 65.66.67.10)
+   - A fully qualified domain name (e.g., peer6.example.com)
+   - username@domain (e.g., roaming@sexample.com)
+   - The wildcard %any

To establish a Pluto IKE connection, two peers must either have a common shared-secret key or a valid RSA key in their configuration files.

The PSK literal stands for *pre-shared key* and signals the fact that a common secret is to be used for endpoint authentication. The secret then follows and it must be enclosed in double quotes; the secret can be any string of any length as long as it is identical on both ends of the IKE connection. However, I recommend that you make the secret at last 256 bits long. To generate an appropriate shared secret, you can use the FreeS/WAN-supplied `ipsec` utility in the following form:

```
[ramon]$ ipsec rambits 256
```