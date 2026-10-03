OpenSSH, SSH certificate authorities are useful for verifying host keys when connecting between servers.

Don’t even consider deploying an OpenSSH CA unless you can automatically distribute files to all your servers and remotely restart sshd on them. If you don’t have automation in place, take a look at Ansible or one of its competitors.

An SSH CA has a whole bunch of functions that are only useful in edge cases. An organization like Google or Facebook needs a whole bunch of features that most of us don’t. Read the ssh-keygen(1) man page for the full range of CA options. Here we’ll set up a comparatively simple CA for a middle-sized network, starting with the simpler host certificates, then proceeding to the more complex user certificates.

# Certificate Expiration

A critical part of signed certificates is that they expire. Yes, you could set all of your certificates to be good for a quarter-century, but those keys will be insecure long before that. Plan from the beginning to use your automation system to regularly update your certificates.

Attacking public keys computationally, in the absence of a flawed implementation, can take billions of years. Software has bugs, though, and it’s possible that a bug might let an intruder crack a key in much less time. Also, those aeons needed to computationally break a key are averages. The intruder might get lucky. Eternally valid certificates increase the intruder’s chances of success.

How long should a certificate be good for? Rolling over certs every year or so is most common. If you have one of those orchestrated networks where servers appear and disappear by the magic of automatic deployment, you might want to regenerate your host key certificates every week or month.

In short, never plan to use certificates longer than a year, except in those rare cases where a host cannot be changed. No, I don’t mean “the boss would really like this host to never change,” I mean “the federal government has declared this host a life-sustaining service and changing the certificate is a felony that carries a minimum jail sentence.”

Don’t set your certificates to expire in exactly one year, though. Remember, life happens. Maybe you put on your calendar to renew all of your certificates in 52 weeks, but you develop appendicitis the day before and you’re off work for three weeks. I allow at least a month of leeway for such emergencies, so these examples assume we expire all certificates in fifty-six weeks and five days.

Better still? Use your automation system to renew and replace all certificates