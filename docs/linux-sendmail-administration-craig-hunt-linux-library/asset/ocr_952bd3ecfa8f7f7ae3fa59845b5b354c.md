mailer is a valid mailer defined by a command. host will handle this mail, and user is the address of the e-recipient. An example of this syntax taken from the sample sendmail.cf file is:

```
R$ < @$ > $ $ #smtp $2 $: $1 < @ $2 $3 user@host.domain
```

The comment user@host.domain at the end of this rule implies that the pattern will match addresses of this format. That's almost true. The addresses have already been through the canonify ruleset before they reach ruleset 0, so the input address will be “focused” with angle brackets. For the e-mail address kathy<wren.foobirds.org would match the pattern and be processed by this rule. The address matches pattern*$ because:

+   - The address has zero or more tokens (the token kathy) that match the first $* symbol.
- The address has a literal <@.
- The address has one or more tokens (the five tokens wren.foobirds.org) that match the requirement of the second $* symbol.
- The address has a literal >.
- The address has zero or more—in this case, zero—tokens that match the requirement of the last $ symbol.

This pattern produces two indefinite tokens. Indefinite token $1 contains kathy and $2 contains wren.foobirds.org. No other matches occurred, so $3 is empty. These indefinite tokens are used to rewrite the address into the following triple:

```
$#smtp wren.foobirds.org $: kathy@wren.foobirds.org>
```

The components of this triple are:
$smtp is the internal name of the mailer that delivers the message.
$@ wren.foobirds.org wren.foobirds.org is the recipient host.
$: kathy@wren.foobirds.org kathy@wren.foobirds.org is the recipient user.

The mail delivery triple is just that—three pieces of information needed to deliver the mail, including the mailer name, the host, and the e-mail address. The mail delivery is created in ruleset 0. Sometimes, however, a template that looks like a mail delivery triple is used for another purpose. These variations on the mail delivery triple can appear in any ruleset.