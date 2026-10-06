# Defining User Policies

Hashing passwords leads to the use of an interesting hacking technique called the rainbow table. A rainbow table contains all the possible hashes of all the key combinations that might have been used in a password, up to a given size. For example, all the single-character combinations are hashed, all the two-character combinations are hashed, and so on up to some finite limit (often 8 to 10 characters). If you get the SAM file then you can search the rainbow table for matches. If you find a match, then the associated plaintext must be the password. Tools such as OphCrack boot into Linux and then run a rainbow table against the SAM file. Larger rainbow tables are cumbersome. No current rainbow tables handle passphrases of 20 characters or more.

You can find a good reference for this discussion at http://www.passwordanalytics.com/theory/security/rainbow-table.php.

# Internet Use Policy

Most organizations provide users with some sort of Internet access. There are several reasons for this. The most obvious reason is e-mail. However, that is hardly the only reason to have Internet access in a business or academic setting. There is also the web, and chat rooms. All of these can be used for legitimate purposes within any organization but can also be serious security problems. Appropriate policies must be in place to govern the use of these technologies.

The web is a wonderful resource for a tremendous wealth of data. Throughout this book we have frequently referenced websites where one can find valuable data and useful utilities. The Internet is also replete with useful tutorials on various technologies. However, even nontechnologyrelated business interests can be served via the web. Here are a few examples of legitimate business interests of the web:

+   * Sales checking competitors' websites to see what products or services they offer in what areas, perhaps even getting prices
* Creditors checking a business’s AM Best or Standard and Poor’s rating to see how their financial rating is doing
* Business travelers checking weather conditions and getting prices for travel

Of course, other web activities are clearly not appropriate on a company’s network:

+   * Using the web to search for a new job
* Any pornographic use
* Any use which violates local, state, or federal laws
* Use of the web to conduct employee’s own business (i.e., an employee who is involved in another enterprise other than the company’s business, such as eBay)