# OffSec

Penetration Testing with Kali Linux

2050_toprules_0_F.rule

Listing 273 - Listing of Hashcat's rule files

These predefined rules cover a broad variety of mutations and are most useful when we don't have any information about the target's password policy. We'll use the predefined rules in the upcoming demonstrations and examples. However, it's always most efficient to discover information about existing password rules, or to look up typically-used default policies for the target software environment.

Let's summarize what we did in this section. We began discussing rule-based attacks and why they are preferred over dictionary attacks. Then, we discussed rules and used them to mutate wordlists to crack an MD5 hash. At the end of this section we briefly introduced the predefined rules by Hashcat.

In the next section we will discuss a basic methodology for cracking, which we can use as an outline for demonstrations and examples.

# 13.2.3 Cracking Methodology

In the next sections we'll walk through the various phases of a real-world password-cracking session, beginning with an overview of a solid methodology.

We describe the process of cracking a hash with the following steps:

+   1. Extract hashes
2. Format hashes
3. Calculate the cracking time
4. Prepare wordlist
5. Attack the hash

The first step is to extract the hashes. In a penetration test we'll find hashes in various locations. For example, if we get access to a database system, we can dump the database table containing the hashed users.

The next step is to format the hashes into our tool's expected cracking format. To do this we'll need to know the hashing algorithm used to create the hash. We can identify the hash type with hash-identifier⁶³¹ or hash-hashid⁶³² which are installed on Kali. Depending on the hashing algorithm and the source of the hash, we may need to check if it is already in the correct format for our cracking tool. If not, we need to use helper tools to change the representation of the hash into the expected format of our cracking tool.

In the third step, we will determine the feasibility of the cracking attempt. As we discussed before, the cracking time consists of the keyspace divided by the hash rate. If the calculated cracking time exceeds our expected lifetime, we might reconsider this approach!

> ⁶³¹ (Kali Tools, 2022), https://www.kali.org/tools/hash-identifier/
⁶³² (Kali Tools, 2022), https://www.kali.org/tools/hashid/

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

398