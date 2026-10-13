See the sendmail documentation for more information on the use of `access_db`.

*I run a mail server. A local company asked if we could swap services, us as a secondary email server for them and they for us in case one of our mail systems goes down. Do I need to do anything special?*

Short answer: no. The only thing that needs to happen is each of you will need a second MX entry in your DNS records specifying the other sendmail system, and with a higher priority. You should not just arbitrarily add someone else’s mail server as a secondary without asking first, however.

*I’m using GnuPG and I occasionally use it when someone needs to send me confidential information. But I forgot what my pass phrase is. Can I recover it?*

Unfortunately, no. What you’ll need to do is immediately create a new private and public key pair using the method discussed in this chapter and contact anyone who has your old key and give them your new one. Don’t forget to do this if you’ve put your public key on a key server.