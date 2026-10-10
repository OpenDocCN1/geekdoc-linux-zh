# THE COMMAND FILE FORMAT

Entries in a Netscape Signing Tool command file have this general format:

keyword=value Everything before the = sign on a single line is a keyword, and everything from the = sign to the end of line is a value. The value may include = signs; only the first = sign on a line is interpreted. Blank lines are ignored, but white space on a line with keywords and values is assud to be part of the keyword (if it cos before the equal sign) or part of the value (if it cos after the first equal sign). Keywords are case insensitive, values are generally case sensitive. Since the = sign and newline delimit the value, it should not be quoted.

# Subsection

basena

+   - Sa as -b option.

compression

+   - Sa as -c option.

certdir

+   - Sa as -d option.

extension

+   - Sa as -e option.

generate

+   - Sa as -G option.

installScript

+   - Sa as -i option.

javascriptdir

+   - Sa as -j option.

htdir

+   - Sa as -J option.

certna

+   - Nickna of certificate, as with -k and -l -k options.