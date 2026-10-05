# OffSec

# 13.4 Wrapping Up

As penetration testers, we must familiarize ourselves with a variety of password attacks. We can leverage these attacks in an external assessment to breach a perimeter via exposed network services. We can also leverage them in internal penetration tests to retrieve plaintext passwords or use hashes to access other systems. These are important skills for the Active Directory Modules we'll discuss later in this course.

In this Module, we first attacked network services using basic dictionary attacks. Then, we discussed the cracking process and rule-based attacks. We used these techniques to crack a KeePass password manager database and an SSH private key. In the last Learning Unit, we worked with NTLM and Net-NTLMv2 hashes, cracking them and using them to gain access to another system by passing the NTLM hash or relating Net-NTLMv2.

In conclusion, we should remember the prevalence of password attacks from an offensive perspective. In a majority of real-life penetration tests, we won't breach a perimeter with technical exploits but rather client-side or password attacks. We should also be aware that the skills from this Module are not only useful from an offensive perspective, but also provide insight into how to build an effective and well-rounded defense.