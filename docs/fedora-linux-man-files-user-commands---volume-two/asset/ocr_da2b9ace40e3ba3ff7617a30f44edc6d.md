# OUTPUT

Output is generated for each element described in the previous section. Output is done in the same order as the elements are specified in the input, except for non-option parameters. Output can be done in *compatible (unquoted)* mode, or in such way that whitespace and other special characters within arguments and non-option parameters are preserved (see **QUOTING**). When the output is processed in the shell script, it will seem to be composed of distinct elements that can be processed one by one (by using the shift command in most shell languages). This is imperfect in unquoted mode, as elements can be split at unexpected places if they contain whitespace or special characters.

If there are problems parsing the parameters, for example because a required argument is not found or an option is not recognized, an error will be reported on stderr, there will be no output for the offending element, and a non-zero error status is returned.

For a short option, a single `-'` and the option character are generated as one parameter. If the option has an argument, the next parameter will be the argument. If the option takes an optional argument, but none was found, the next parameter will be generated but be empty in quoting mode, but no second parameter will be generated in unquoted (compatible) mode. Note that many other (1) implementations do not support optional arguments.

If several short options were specified after a single `-'`, each will be present in the output as a separate parameter.

For a long option, `--' and the full option name are generated as one parameter. This is done regardless whether the option was abbreviated or specified with a single `-' in the input. Arguments are handled as with short options.

Normally, no non-option parameters output is generated until all options and their arguments have been generated. Then `--' is generated as a single parameter, and after it the non-option parameters in the order they were found, each as a separate parameter. Only if the first character of the short options string was a `-'`, non-option parameter output is generated at the place they are found in the input (this is not supported if the first format of the **SYNOPSIS** is used; in that case all preceding occurrences of `-' and `+' are ignored).