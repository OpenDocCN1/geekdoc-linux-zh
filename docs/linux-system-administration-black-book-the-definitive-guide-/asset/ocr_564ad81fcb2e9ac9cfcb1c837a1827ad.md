# Chapter 12 Internet Email: sendmail + lDA

The Date header is part of a small group that refers to date and time information. It is the only header item in its group that is standard for email use. This header specifies either when the mail was written or when the mail was passed to the sender's mail server, depending on how this server is set up.

After the Date header is a pair already covered in the Sender And Recipient Indication headers in Table 12.3:

+   - To: "Diane Smith" <dsmith@inventors.com>
+   - From: Mary Smith <msmith@spices.com>

The following is a miscellaneous header type:

+   - Subject: Movies

It is listed with its cousins in Table 12.4.

Another item already mentioned is the In-Reply-To header, which tells you which email this particular mail was written in response to:

+   - In-Reply-To: <NOBB LM LFK LJ PNF AH B B D I E EKJCHAA.dsmith@inventors.com>

After this is another header that is the only one in its class that is standard for email use:

+   - Mīme-Version: 1.0

This header contains information about which MIME standard the message was formatted to adhere to. Finally, the following line ends the mail header:

+   - Content-Type: text/plain; charset=“us-ascii”; format=flawed

Content-Type is one of two headers used in email among the Encoding Information type of headers:

# Table 12.4 Miscellaneous mail header fields.

| Header | Purpose |
| Comments: | Includes meta-information about the mail message. Should be enclosed in parentheses. |
| Content-Description: | Often contains labels for attached files. |
| Keywords: | Includes comma-separated terms or phrases used for database searches. |
| Subject: | Specifies the email's topic. |