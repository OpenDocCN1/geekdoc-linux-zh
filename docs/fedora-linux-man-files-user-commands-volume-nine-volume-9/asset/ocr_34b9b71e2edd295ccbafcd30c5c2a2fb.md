# ## ENVIRONMENT

# ### SSH_USE_STRONG_RNG

The reseeding of the OpenSSL random generator is usually done from **/dev/urandom**. If the **SSH_USE_STRONG_RNG** environmt variable is set to value other than **0** the OpenSSL random generator is reseeded from **/dev/random**. The nuer of bytes read is defined by the SSH_USE_STRONG_RNG value. Minim is 14 bytes. This setting is not recommended on the computers without the hardware random generator because insufficient entropy causes the connection to be blocked until enough entropy is available.