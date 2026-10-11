```
```
}
printf '<strong>Name: %s</strong><br />\n', Format_name ($entry_ref);
my $address = '';
$address .= $entry_ref->{street};
if defined ($entry_ref->{street}) {
$address .= ', ' . $entry_ref->{city};
if defined ($entry_ref->{city});
$address .= ', ' . $entry_ref->{state};
if defined ($entry_ref->{state});
$address .= ' ' . $entry_ref->{zip};
if defined ($entry_ref->{zip});
print "Address: $address<br />\n"
if $address ne "";
print "Telephone: $entry_ref->{phone}<br />\n"
if defined ($entry_ref->{phone});
print "Email: $entry_ref->{email}<br />\n"
if defined ($entry_ref->{email});
print "Interests: $entry_ref->{interests}<br />\n"
if defined ($entry_ref->{interests});
print '<br />\n"';
}
```
```

The function produces output that looks like this:

```
```
<strong>Name: Mike Artel</strong><br />
Address: 4264 Lovering Rd., Miami, FL 12777<br />
Telephone: 075-961-0712<br />
Email: mike.artel@venus.org<br />
Interests: Civil Rights,Education,Revolutionary War<br />
<br />
```
```

The reason for using<br />rather than<br />is to write the document as well-formed XHTML, which is more strict than HTML. Some distinctions between HTML and XHTML are discussed briefly in Section 8.4.2.2, “Producing Web Output.”

The last modification needed for gen_afr.pl is to add to the switchbox another element that points to the HTML-writing functions. The modified switchbox looks like this, where the final element defines a format named html that points to the functions that produce the various parts of an HTML document:

```
```
# switchbox containing formatting functions for each output format
my $switchbox =
{
'text' => # functions for plain text format
{
'init' => undef, # no initialization needed
'entry' => \&text_format_entry,
'cleanup' => undef # no cleanup needed
},
```
```