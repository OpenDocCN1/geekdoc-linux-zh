# ColLabName

The CollabName element holds the name of a collaborator.

The CollabName element uses common attributes.

Example:

See Collab element example.

# ConfDates

The ConfDates element holds the dates of a conference and is often used for holding information about a conference at which a document was presented. For instance, if a DocBook article was written for a conference held from August 1 to August 3, 2000, that information could be listed using this element. This element can also be used for discussing a conference in the text of a document.

The ConfDates element uses common attributes.

Example:

See ConfGroup example below.

# ConfGroup

The ConfGroup element holds other elements that provide information about a conference.

The ConfGroup element uses common attributes.

```
<!DOCTYPE confgroup PUBLIC //OASIS//DTD DocBook V4.1//EN>
<confgroup>
<confdates>March 29, 2001</confdates>
<conftitle>Denver 2001</conftitle>
<confnum>2</confnum>
<address>Denver, Colorado USA</address>
<confsponsor>Linux Weekly News</confsponsor>
</confgroup>
```

# ConfNum

The ConfNum element holds the conference number and is useful when a conference is held regularly.

The ConfNum element uses common attributes.

Example:

See ConfGroup element example.