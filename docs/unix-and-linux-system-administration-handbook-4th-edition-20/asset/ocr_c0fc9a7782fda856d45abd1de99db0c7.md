# Chapter 17 DNS: The Domain Name System

type for the same host). The public zone-signing key verifies the signatures and is included in the zone's data in the form of a DNSKEY resource record.

Parent zones contain DS records that are a hash of the child's self-signed signing key DNSKEY records. A name server verifies the authenticity of a child's DNSKEY record by checking it against the parent zone's signature. To verify the authenticity of the parent zone's key, the name server can check the parent's parent, and so on back to the root. The public key for the root zone would be widely published and included in the root hints file.

The DNSSEC specifications require that if a zone has multiple keys, each is tried until the data is validated. This behavior is required so that keys can be rolled over (changed) without interruptions in DNS service. If a DNSSEC-aware name server queries an unsigned zone, the unsigned answer that comes back is accepted as valid. But problems occur when signatures expire or when parent and child zones do not agree on the child's DNSKEY record.

Before we jump into the mechanics of generating keys and signing zones, we need to outline the real-world status of DNSSEC and its impact on sysadmins. It is ready to deploy, but a couple of problems remain. On the plus side:

+   - Current versions of the DNS software (both named and nsec/bound) are ready. Tools exist to sign zones and verify signatures.

+   - Momentum toward signed zones is building. As of 2010, .gov, .org, and all ccTLDs (mostly in Europe) are now signed. (Sweden was the first signed TLD.) The root will be signed in 2010, and the other gTLDs will follow a year or two later. The U.S. government has required all sites within .gov to be signed

+   - The IETF standards seem to be functional and deployable.

However with the root and TLDs not, the chain of trust is broken. Those that want to sign their zones find other ways to publish their keys. A lookaside validation scheme (RFCs 4431 and 5074) by Sam Weiler of Sparta allows enabling third-party organizations as ISC to validate sites' keys. This is a good interim solution, but also a single point of failure. ISC is used for running critical servers (the F root server), but accidents happen. There are also potential privacy issues with a third party having knowledge of all the sites users visited. (Of course, these same privacy concerns apply to all root server operators.) Another interim solution is the solution of so-called ITARS (itar.iana.org); see page 661.

Strong keys are long, and some sites like to distribute several of them. This means bigger packets. DNSSEC requires EDNS0, the extended DNS protocol, which supports UDP packets larger than 512 bytes. However, not all implementations support it; those folks may not be able to use DNSSEC.