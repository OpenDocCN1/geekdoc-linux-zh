![](bbox=[0.067, 0.1, 0.929, 0.432])

One final note in case your following becomes popular. Mastodon caches data from other instances, where your users' followers are, and this cache can grow rapidly. Avoid any problems by adding the following to the mastodon user's crontab:

```
RAILS_ENV=production
@daily cd /home/mastodon/live && /home/
mastodon/.rvm/shims/bundle exec rake
mastodon:media:remove_remote
```

Ever since Yahoo!'s acquisition of Flickr in 2005 and YouTube's assimilation to the Google empire in 2006, smart people have raised concerns about how their pictures and moving pictures are used. In our exclusive LXF222 interview Cory Doctorow talked about his horror at the new terms that were foisted upon users following Flickr's Yahoo!-ification. Users were forced to associate their Flickr account with a Yahoo! one, or they'd be unable to access their images. Furthermore, content becoming subject to US Federal Law, rather than Canadian Law, was a major concern. Add to that Yahoo! managed to divulge personal data of some three billion accounts (basically anyone that ever had an @yahoo.* email address) in 2013. Yahoo! was acquired by Verizon which subsequently sold off Flickr, not to mention the majority of their other assets. But the concern endures.

# And another thing…

Now let's turn to Google, and in particular its unifying privacy policy edit of 2012. Ostensibly it's made its services (at the time there were about 60, and most people used at least one) simpler to use, but it also afforded them a tremendous amount of data insight. Before, data relating to each service was siloed, so while it was still collecting huge amounts of data from scanning emails (it no longer does this), keeping track of searches, and running all kinds of nebulous algorithms on YouTube uploads, there was no attempt

to correlate across these services. After the fact, users had a choice: either let Google associate all this data with a single identity, or stop using Google's services altogether. Today, with about two billion phones using Android phones all associated with a Google account and all merely transmitting location data, the problem is stark (that's why I use LineageOS – Ed.).
It's easy to target mega corporations, but it's the whole centralised model that's at fault. A pioneering company with all good intentions (which is exactly what Flickr was) could at any point find itself swallowed up by some awful monster. Data is then effectively held hostage until users bend the knee to whatever unsavoury policies said monster demands. In the decentralised model, if one instance turns rogue, or is taken over by a rogue, then that rogue instance can be blacklisted. If a whole project turns to the dark side, then it would be trivial to fork the software and rebuild the network. LXF

> It works! Although we cheated and used a self-signed certificate and a bogus domain name, but you don't need to know that…

![](bbox=[0.747, 0.56, 0.931, 0.725])

![](bbox=[0.452, 0.715, 0.931, 0.955])