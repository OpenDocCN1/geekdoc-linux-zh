⇒ To add to the CRON schedule any new entries that are in the file crontab, type:
    $ crontab crontab RET

NOTES: The name of the command, crontab, is the same as the file it uses, crontab.

# 27.5 Using Contact Managers

Loosely put, a contact manager is a piece of software that helps you keep track of information about people you may need to contact in the future. In the past, people often called the physical embodiment of these things a "rolodex," which incidentally is a trademarked brand name for the Cadillac of such contact managers, the circular Rolodex that sat atop the desk of every successful 20th century businessman. I hear that many people use them even today.

There are many contact manager programs available; the following recipes show two of the best and easiest methods of managing contact information with Linux.

# 27.5.1 Keeping a Free-Form Address List

The simplest way to keep names and addresses in Linux is to keep them in a text file as a free-form address list; to find an entry, use the search capabilities of tools like grep, less, and Emacs.

This method is useful when you need to keep track of name and address information for many parties, but you don't always keep the same kind of information for each—maybe sometimes a name and phone number, sometimes just a mailing address, sometimes a name and email address. With a free-form address list, each entry contains whatever information you have in the format you want. Separate the entries with a delimiter line of your preference. I happen to use "###," but you can use whatever characters you're comfortable with—just make it a combination that won't appear in the text for any of the entries themselves.