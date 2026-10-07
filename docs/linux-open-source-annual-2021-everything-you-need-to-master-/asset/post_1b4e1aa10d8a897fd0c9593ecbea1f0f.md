
# BACKUP WITH DÉJÀUP

![](img/5f8379eaeda572d04307c37d75b0ba5d_62_0.png)

## Set backup location

You can use Gnome's online accounts to back up to Google Drive, a Nextcloud instance or you can also use a network location like Samba or SSH, or a local folder. We recommend using an external hard drive and unplugging it afterwards. If you use a local folder, be aware that anywhere you choose could be hit by a ransomware attack.

![](img/5f8379eaeda572d04307c37d75b0ba5d_62_1.png)

## Choose what to save

Add any folders outside your home directory you want to include in the backup, and exclude anything that you don't. The ~/.cache folder is not necessary and often takes up lots of space - it's where the cache is stored. If you don't want to exclude -steam, use Gnome's Disk Usage Analyzer as a useful tool for seeing what to save.

![](img/5f8379eaeda572d04307c37d75b0ba5d_62_2.png)

## Install Packages

In order to continue, the following packages need to be installed: 

![](img/5f8379eaeda572d04307c37d75b0ba5d_62_3.png)

## Initiate the backup

Hit the Backup Now. You may be prompted to install Duplicity and you will be prompted for a password. If you use one (encrypting off-site backups is a good idea) then for pity don't forget to tell it. In fact, just use a password manager, like we tell you in the future. Click the forward button and start to secure that your files are safe.

![](img/5f8379eaeda572d04307c37d75b0ba5d_62_4.png)

## Set up a schedule

Just as with, regular practice is the key to backup heaven. The Scheduling tab allows you to choose the frequency and longevity of backups. If you backed up to a location that isn't available when an automatic backup initiates, you'll be warned. Be aware of running out of space - old backups will be silently removed in this event, which may not be.

![](img/5f8379eaeda572d04307c37d75b0ba5d_62_5.png)
![](img/5f8379eaeda572d04307c37d75b0ba5d_62_6.png)

## Set be to sure

This is optional, but belt-and-braces approach is always good if you truly care about your data. Consider manually copying your encrypted backups elsewhere: like a USB key, your home server, somewhere in the cloud, it demands matter. Redundancy is good and since you encrypted your backups (you?), losing the shouldn't be a concern.

## Test your backups

Making backups is all well well, but you need to be sure they are viable and that you know the drill for them. Click the Restore button, plug in your storage device if you have done it, click your backup location and choose the date to restore. The most recent one is shown. For this test, restore to a software identifier so known.

## Anatomy of a ransomware attack

Ever wondered how this high-tech financial half-jacking and data scrambling works? Wonder no more.

Unfortunately, if you fall victim to a ransomware attack and don't have backups, it is probably too late to do anything about it. The usual ask price is around $500, though many variants will threaten to delete any amount after a couple of days, and even then make decryption impossible later. These threats provoke anxiety in the victim, who then is more likely to pay before considering the merits of the deal.

What is important to remember is that there's a possibility that whatever control of this malware is reasonable enough to recover a decryption key, there's also the possibility that they won't. Their model, all for, is called why you should better with the extra strain of sending an email after that is achieved? It's not like people who receive a key that will maintain control of strain malware to their friends. That be as it may, whether or not you have access to a decryption key probably exists. There is case of malware that deletes everything – this class of malware is known as a distinct category in D&B – but it doesn't offer criminals much in the way petty ransomware either it gets it and is it possible to recover a decryption key without a mention of ransom? It's necessary to understand all this possible, how key malware mechanics (ha – ed).

Traditional symmetric encryption requires two people to agree on a secret key by meeting in the flesh, or via sealed message be delivered by a trusted intermediary. Today's numerous, electronic transactions do not allow such luxury. The key to our buddy at paypal everytime we want to pay for something: every transaction requires a new key to be

Frequently now we have no way to share a secret with another party. Public asymmetric encryption which enables us to share a secret with another other a person or a machine that we have never met before, which is what underlies the key-exchange part of SSL/TLS (using in HTTPS), SSH and PG communications. Public key crypto is also intrinsic, to the workings of all encryption. It's a bit of a leap, and also a concept to get your around, but we will leave you to point it out of here (or check out LFY). If you need to share a secret between two parties to hold a set of keys – only one of them needs to be secret; and random numbers are used.

## MAKES YOU WANCRY

The WannaCry damage could have been much worse if not for the actions of one hacker (a security researcher) who noticed WannaCry was trying to capture a secret at an unregistered domain. He registered the domain and captured the secret, which had the effect of neutering the malware. Once infected machines were unable to connect to this domain the threat stopped. In other markets, hackers found no success.

Further variants of WannaCry appeared in the aftermath, and more killchain variants were found. These hackers, because of a huge mistake in August 2017 he was in Las Vegas while the story was out attending the Def conference, and was promptly picked by the FBI on hacking charges related to Kronos bank. ever saved and We've learned that technology is moving faster than laws can keep with. They are bound by a treaty known as the Wassenaar Arrangement, which makes regulations governing software that could be misused. The agreement was reached in December 2017 to make possible for security researchers, who have previously researched vulnerabilities.

| How encryption works |
| :--- |
| Symmetric encryption uses the same key for both encryption and decryption. Asymmetric encryption uses a pair of keys: a public key for encryption and a private key for decryption. If you encrypt a message with the public key, only the private key can decrypt it. |

```python
from cryptography.hazmat.primitives.asymmetric import rsa
from cryptography.hazmat.primitives import padding
from cryptography.hazmat.primitives import hashes

# generate keys
private_key = rsa.generate_private_key(public_exponent=65537, key_size=2048)
ublic_key = private_key.public_key()

# encrypt
message = b"This is a secret"
ciphertext = public_key.encrypt(
    padding.OAEP(mgf=padding.MGF1(hashes.SHA256()), algorithm=hashes.SHA256(), label=None),
    message
)

# decrypt
drypted = private_key.decrypt(
    padding.OAEP(mgf=padding.MGF1(hashes.SHA256()), algorithm=hashes.SHA256(), label=None),
    ciphertext
)
```

You're unlikely to see a secret like this on Linux, or such a high demand - but you know.

![](img/5f8379eaeda572d04307c37d75b0ba5d_64_0.png)

Ransomware that phones home to central server use symmetric encryption to perform sordid garbling. A random key and a unique identifier could be generated on the target machine and both of these are then stored on that command and control (CC) server. All traces of the key will be removed from the victim's machine once files have been duly scrambled, and the unsuspecting victim then sends requested ransom, together with their unique identifier to the extortionist.

Said extortionist, if they had any hint of decency, would then provide the decryption key and life would go on on some degree of decentralisation: somewhere there a list of keys and tokens to be stored. For large-scale attacks this isn’t ideal – multiple command and control servers are used for reduction – and it makes sense to somehow store those keys locally. This turns into a Catch-22 cascade of futility. If you encrypt the key and store it locally, but then where do you use used to encrypt the key?

Instead, an attacker could use a hybrid scheme whereby the symmetric key (or keys) used to scramble all the files is stored on the victim's machine, asymmetric implementation of such scheme would require our attacker to only use a single private key, while the public key could be stored locally – inside the program.

So in order to recover their files, the victims need to pay the ransom, which involves the attacker's private key, which is combined with the two keys to decrypt the stored symmetric key. Simple, right? Whoever said these people don’t have money the victims aren’t much worse off. Hospitals, and other vital organisations, ought to have a backup regimen in place, but restoring a whole network under pressure is a complex business. How long would it take to restore your machine's software, configuration and data if it was wiped, multiply this number by at least several hundred

# HOW TO BLACKMAIL PEOPLE

> Ransomware that phones home to central server use symmetric encryption to perform its sordid garbling.

## Scum, vile scum

Actually, they don’t. Ransomware and control servers can be hosted/rented via the dark web and all the day management business can be taken care of with a few clicks in a friendly interface. Having a single key governing all infections is not a small threat as one might think, as it is delivered from the CC server to the victim's machine over HTTPS or SSH, but it is easily mitigated by researchers.

There have been number of high-profile cases where ransom has been paid and data has been released. In 2016, an Australian company Angou paid $17,000 (at the time) after being infected with the ransomware. In or without death situations, it is easy to see why paying the ransom for a possible operation may be worth more than the cost of doing work around a crippled network.

Even if they don’t provide a decryption key, the ransom may be demanded by these costly, so from an accounting (but not necessarily principled) point over 2016 to all the (then)-most pieces of malware in the world, eventually being located in 30 different languages and no longer requiring infrastructure – if it’s located in a friendly jurisdiction, is easy for authors to do out once it becomes prevalent.

Some malware is selective about what it encrypts: it may just encrypt (based on file extensions) and leave the rest of the OS data. This means only requires permissions to run. If you are lucky means it’s easy to clean up, at least the source of the infection is drawn down and so as backups are taken. Of course people have come up including filing scripts and getting these infections to recover themselves. There’s nothing more

Fileless malware is becoming the new norm. This often travels by posted documents (PDFs in particular) which contain some script or code to fetch hostile code from the internet and inject it directly into memory. This makes it very tricky to detect-
