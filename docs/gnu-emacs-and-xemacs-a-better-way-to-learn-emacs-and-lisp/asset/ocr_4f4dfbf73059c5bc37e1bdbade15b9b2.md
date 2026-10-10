The default openssl command-line arguments should be fine, but the Program Name variable should be set to `emacs-ssl` rather than `openssl`, ensuring that your new shell script is called rather than `openssl` directly. Save the new setting, and kill the Customize buffer.

The subject of SSL is quite involved; legistates vary by country, and several commercial interests demand fees for certificates. The WWW is your best source of up-to-date information on this rapidly changing area. The OpenSSL site, mentioned in the preceding section, and the W3 Consortium's site (no relation to the Emacs W3) are good starting points: `http://www.w3.org`.

# # Cookies

Cookies are controversial. Some people consider them evil violations of privacy, and others feel that they are nothing to worry about. These are files that have no meaning to any program on your system but serve to identify you to a previously visited WWW host the next time you visit. Registration and password information is stored in cookies. The result is that the next time you visit a site you won't need to manually log in.

Cookies are enabled in W3 by default. You can prevent W3 from accepting any cookies with this line in `~/.w3/profile`:

```
```lua
(set-q-default 'url-privacy-level 'paranoid)
```
```

You can use Customize to tailor W3's cookie behavior in more subtle ways. Figure 20.5 shows the Url Customize Group buffer. The Privacy Level checkboxes give you a range of levels from which to choose. Summon this buffer by pressing M-x and typing `customize-group`.

At the minibuffer prompt, type `url`

Alternatively, respond to the prompt with `url-cookie`

You will see in this new Customize buffer INS buttons next to the two items Trusted Urls and Untrusted Urls. Click on one of these buttons with the middle mouse button, and a new text entry field will open. You can then type in either regular expressions (which can include or exclude ranges of URLs) or actual specific URLs, as shown in Figure 20.6.