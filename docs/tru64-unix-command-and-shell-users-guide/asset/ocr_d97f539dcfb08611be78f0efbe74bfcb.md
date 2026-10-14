In addition to the 12-hour/24-hour clock differences, punctuation for written times can vary, for example:

3:20 p.m. (United States)

15h20 (France)

15.20 (Germany)

15:20 (Japan)

See the date(1) reference page for a discussion of the date and time formats available, and their usage.

# C.2.3 Numeric and Monetary Formats

The characters used to format numeric and monetary values vary from place to place. In the United States, the convention is to use a period (.) as the radix character (the character that separates whole and fractional quantities), and a comma (,) as the thousands separator. In many European countries, these conventions are reversed. For example:

1,234.56 (United States)

1.234,56 (France)

Here are some sample formats for monetary items:

$1,234.56 (United States, dollars)

kr1.234,56 (Norway, krona)

SFrs.1,234.56 (Switzerland, Swiss francs)

Some formats for monetary amounts include more than two places for fractional digits.

# C.2.4 Messages

Programs are sometimes written with English messages embedded in the program itself. In an internationalized program, messages are kept in a separate file and replaced in the program with calls to a messaging system. Messages kept in a separate file can be translated and made available to the program. When translated messages are available, users can interact with the system in their local language.

# C.2.5 Yes/No Prompts

Many programs ask questions that need a positive or negative response. Those programs typically look for the English string literals y or yes, n or no. An internationalized program lets users enter the characters or words