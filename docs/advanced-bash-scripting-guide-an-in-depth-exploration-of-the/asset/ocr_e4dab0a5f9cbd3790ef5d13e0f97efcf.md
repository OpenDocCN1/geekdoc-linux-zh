# Advanced Bash-Scripting Guide

Mariusz Gniazdowski contributed a hash library for use in scripts.

# Example A-20. Library of hash functions

```
# Hash:
# Hash function library
# Author: Mariusz Gniazdowski <mariusz.gn-at-gmail.com>
# Date: 2005-04-07

# Functions making hashes in Bash a little less painful.
```

+   * Limitations:
* Only global variables are supported.
* Each hash instance generates one global variable per value.
* Variable collisions are possible
* If you define variable like __hash_hashname_key
* Keys must use char that can be part of a Bash variable name (no dashes, periods, etc.).
* The hash is created as a variable:
  * hashname_keyname
* So if someone will create hashes:
  myhash + mykey = myhash_mykey
  myhash + _mykey = myhash_mykey
Then there will be a collision.
(This should not pose a major problem).

Hash_config_varname_prefix=__hash_

```
# Emulates: hash[key]=value

# Params:
# 1 - hash
# 2 - key
# 3 - value
function hash_set {
  eval "${Hash_config_varname_prefix}${1}_$(2)=\${$3}"
}
```

```
# Emulates: value=hash[key]

# Params:
# 1 - hash
# 2 - key
# 3 - value (name of global variable to set)
function hash_get_into {
  eval "\${Hash_config_varname_prefix}${1}_$(2)=\${$3}"
}
```

```
# Emulates: echo hash[key]

# Params:
# 1 - hash
# 2 - key
# 3 - echo params (like -n, for example)
function hash_echo {
```

# Appendix A. Contributed Scripts