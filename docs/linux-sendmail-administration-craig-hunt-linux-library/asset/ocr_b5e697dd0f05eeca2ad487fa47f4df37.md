# Formatting Headers

In addition to modifying the mail addresses to make them correct for the mail delivery program, Sendmail ensures that all of the headers required by the mail delivery program are provided and are properly formatted. As noted above, the flags in a mailer definition identify the headers required for that mailer.

The Sendmail configuration file contains header templates that define the proper format for the various message headers. Each template has an associated flag. If a matching flag is found in the mailer definition, Sendmail knows that the mailer requires that particular header and adds it if it is not already contained in the mail message. The mail headers contained in the message Sendmail receives from the MUA are maintained and forwarded to the mail delivery program. The flags and the header templates ensure that all of the required headers are provided even if the MUA fails to provide them.

The role of a message submission agent is central to what Sendmail does. Sendmail receives mail from the user's mail program, selects the correct mail delivery program for that, and properly formats the message headers and e-mail addresses for the selected mailer. The MSA function is very complex and it is the focus of most Sendmail configurations. Despite its complexity, serving as a mail submission agent is not the only Sendmail function.

# A Message Transfer Agent

Sendmail acts as an MTA when it receives mail from an external system as it is not the first-hop MTA and it doesn't modify the mail message. Therefore, Sendmail isn't acting as an MSA. The mail may be inbound mail destined for someone on the local system or mail being relayed through the local system to a remote server.

Sendmail is designed to deliver mail to the correct recipient. Outbound mail is handled by formatting and passing it to the correct mailer for delivery. Inbound mail is handled by passing it to the correct user or system.

In certain circumstances, inbound mail needs to be forwarded before final delivery can be made. The To: address on the mail may be an alias for the real recipient. The recipient may define private forwarding for their mail. It is even possible that the hostname in the To: address is not the name of the local host and that the mail needs to be forwarded to a remote host for delivery. Three Sendmail features, *aliasing*, *forwarding*, and *relaying*, handle these three types of delivery.