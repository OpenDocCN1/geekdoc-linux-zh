the following controlchan entry specifies the external program `/usr/lib/news/bin/controlchan` to handle all control messages, except cancel messages (meant for canceling an article):

controlchan!\
:\*, control, control.\*, !control.cancel\
:Tc, Wsm, /usr/lib/news/bin/controlchan

In addition to these feed entries, you add entries for any actual sites to which your news server provides news feeds. Such entries have the format

feedme.domain.com\
:!junk, \control!foo\
:Tm: innfeed!

where *feedme.domain.com* is the fully qualified domain name of the site to which your system sends news articles.

# ## The incoming.conf file

The *incoming.conf* file describes which hosts are allowed to connect to your host to feed articles. For a single feed, you can add an entry like

peer mybuddy {
    hostname: a-feed-site.domain.com
}

where *mybuddy* is a label for the peer and *a-feed-site.domain.com* identifies the site that feeds your site.

![](bbox=[0.15, 0.62, 0.22, 0.69])

Keep in mind that simply adding a site’s name in the *incoming.conf* file does not cause that remote site to start feeding news to your site — it simply enables your server to accept news articles from the remote site. At the remote site, your buddy has to configure his or her server to send articles to your site.

# ## The readers.conf file

This file specifies the host names or IP addresses from which newsreader clients (such as Mozilla) can retrieve newsgroups from your server. For example, the following *readers.conf* file allows *read access* and *post access* (meaning you can submit articles) from *localhost* and from any host in the network 192.168.0.0:

auth "localhost" {
    hosts: "localhost, 127.0.0.1, stdin"
    default: "<localhost>"
}