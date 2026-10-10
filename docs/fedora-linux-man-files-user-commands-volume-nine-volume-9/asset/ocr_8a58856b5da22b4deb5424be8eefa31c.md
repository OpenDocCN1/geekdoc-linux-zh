# NOTES

The `MIME` `ssage` `st` `be` `sent` `without` `any` `blank` `lines` `between` `the` `headers` `and` `the` `output.` `So` `mail` `programs` `will` `automatically` `add` `a` `blank` `line.` `Piping` `the` `mail` `directly` `to` `sendmail` `is` `one` `way` `to` `achieve` `the` `correct` `format.`

The `supplied` `sage` `to` `be` `signed` `or` `encrypted` `st` `include` `the` `necessary` `MIME` `headers` `or` `many` `S/MIME` `cllents` `wont` `display` `it` `properly` `(if` `at` `all).` `You` `can` `use` `the` `**text**` `option` `to` `automatically` `add` `plain` `text` `headers.`

A `“signed` `and` `encrypted”` `ssage` `is` `one` `where` `a` `signed` `ssage` `is` `then` `encrypted.` `This` `can` `be` `produced` `by` `encrypting` `an` `already` `signed` `ssage:` `see` `the` `examples` `section.`

This `version` `of` `the` `program` `only` `allows` `one` `signer` `per` `ssage` `but` `it` `will` `verify` `multiple` `signers` `on` `received` `ssages.` `So` `S/MIME` `cllents` `choke` `if` `a` `ssage` `contains` `multiple` `signers.` `It` `is` `possible` `to` `sign` `ssages` `“in` `paral1el”` `by` `signing` `an` `already` `signed` `ssage.`

The `options` `**encrypt**` `and` `**decrypt**` `reflect` `common` `usage` `in` `S/MIME` `cllents.` `Strictly` `speaking` `these` `process` `PKCS#7` `enveloped` `data:` `PKCS#7` `encrypted` `data` `is` `used` `for` `other` `purposes.`

The `**resign**` `option` `uses` `an` `existing` `ssage` `digest` `when` `adding` `a` `new` `signer.` `This` `ans` `that` `attributes` `st` `be` `present` `in` `at` `least` `one` `existing` `signer` `using` `the` `sa` `ssage` `digest` `or` `this` `operation` `will` `fail.`

The `**stream**` `and` `**i nd ef**` `options` `enable` `experimental` `streaming` `L/O` `support.` `As` `a` `result` `the` `encoding` `is` `BER` `using` `indefinite` `length` `constructed` `encoding` `and` `no` `longer` `DER.` `Streaming` `is` `supported` `for` `the` `**encrypt**` `operation` `and` `the` `**sign**` `operation` `if` `the` `content` `is` `not` `detached.`

Streaming `is` `always` `used` `for` `the` `**sign**` `operation` `with` `detached` `data` `but` `since` `the` `content` `is` `no` `longer` `part` `of` `the` `PKCS#7` `structure` `the` `encoding` `remains` `DER.`