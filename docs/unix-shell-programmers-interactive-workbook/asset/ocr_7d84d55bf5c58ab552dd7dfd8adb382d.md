# Appendix B: Built-In Command Reference

# PARAMETER EXPANSIONS

$${parameter:-word}

Use Default Value. If parameter is null or unset, ksh substitutes the expanded value of word. Otherwise, ksh substitutes the value of parameter.

$${parameter-word}

Use Default Value. If parameter is unset, ksh substitutes the expanded value of word. Otherwise, ksh substitutes the value of parameter.

$${parameter:=word}

Assign Default Value. If parameter is null or unset, ksh assigns the expanded value of word to parameter. ksh then substitutes the value of parameter.

$${parameter=word}

Assign Default Value. If parameter is unset, ksh assigns the expanded value of word to parameter. ksh then substitutes the value of parameter.

$${parameter?word}

Display Error. If parameter is null or unset, ksh expands and displays word on standard error, and causes your shell script, if any, to terminate with a return value of False (1). Otherwise, ksh substitutes the value of parameter.

$${parameter?word}

Display Error. If parameter is unset, ksh expands and displays word on standard error, and causes your shell script, if any, to terminate with a return value of False (1). Otherwise, ksh substitutes the value of parameter.

$${parameter:+word}

Use Alternate Value. If parameter is null or unset, ksh substitutes null. But if parameter is not null or unset, ksh substitutes the expanded value of word.

$${parameter+word}

Use Alternate Value. If parameter is unset, ksh substitutes null. But if parameter is not null or unset, ksh substitutes the expanded value of word.