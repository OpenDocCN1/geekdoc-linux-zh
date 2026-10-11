# **Using S/Key Version 1.1b** Given the tools we've compiled (and corrected), we may now implement the S/Key system using `keys`. To begin, we'll establish the user `mary` with S/Key. In the following series of examples, the server system will be called `topcat`. We will perform the following steps as an example:

+   - Initialize `mary` with `keyinit`
+   - Provide `Mary` with a printed list of one-time passwords
+   - Change the default shell in `/etc/passwd` to `/usr/local/bin/keys` for `mary`
+   - Verify that `mary` can successfully login

**Initialize `mary` with `keyinit`.** Example 6-6 shows the system administrator, as `root`, executing the `keyinit` command, on behalf of the user, `mary`, to initialize her OTP list with the S/Key system. This step must be executed prior to `Mary` using the S/Key system. Take note that this command is executed locally on the server. This prevents the secret password from being sent over the network. The execution of `keyinit` has caused the `/etc/skeykeys` file to be updated with a hexadecimal representation of the 99th OTP generated using the given secret password and seed. This is the information required by the server `topcat` to verify the 98th password in the list, which is the password that `Mary` will be prompted for when she first uses S/Key through `keys`. The record for `mary` in the `/etc/skeykeys` file as a result of Example 6-6 is

```
mary 0099 to25065      be94606891aaca86fb Mar 06, 1999 05:25:43
```

The fields in this record are—from left to right—the username, the sequence number of the most recently used OTP, the seed, the 99th OTP in hexadecimal notation, and the date and timestamp reflecting when the record was entered. The pertinent information relating to this record may be viewed with the `keyinfo` script, as shown in Example 6-7. Note that the output of `keyinfo` `mary` displays the sequence number of the *next* required password in the OTP list,

# **Example 6-6** Initializing a User with `keyinit`.

```
```
[root@topcat]# keyinit mary
[Adding mary]
 Enter secret password:
 Again secret password:
 ID mary s/key is 99 to25065
 Next: login password: MOON JADE MAIN LAW OMIT FANG*
[root@topcat]#
```
```

Even though the system claims that this is the next login password, it is actually the 99th OTP and will never be requested; see Example 6-8.

# **Example 6-7** The `keyinfo` Command

```
```
# keyinfo mary
98 to25065
# ```
```