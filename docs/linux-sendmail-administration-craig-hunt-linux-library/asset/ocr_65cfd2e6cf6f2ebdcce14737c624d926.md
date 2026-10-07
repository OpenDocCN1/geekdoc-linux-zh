# 8

# # Understanding Rewrite Rules

Sendmail is essentially a mail router. It receives mail, analyzes the delivery address of mail to determine how the mail should be delivered, formats the mail for delivery by the selected mailer, and hands the mail off to the delivery system, which in some cases is Sendmail itself. At the heart of most of these functions are rewrite rules. Rewrite rules analyze the delivery address, select the correct mailer, and format mail for delivery. About the only things they don't do is collect inbound mail or transport outbound mail. Mastering Sendmail requires mastering rewrite rules. This chapter will give you all the information you need to read, understand, and—when absolutely necessary—write rewrite rules.

The rules are organized into groups of related rules called rulesets that can be called like subroutines by sendmail commands. Certain rulesets are used by Sendmail to process specific types of addresses. Before getting into the details of rewrite rule syntax, let's look at rulesets to gain a global view of how rewrite rules are organized and used.

# ## Basic Rulesets

Grouping rewrite rules into rulesets allows related rules to be referenced by a single name or number. The S command marks the beginning of a ruleset and identifies it with a