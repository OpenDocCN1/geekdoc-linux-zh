# Infrastructure Protocols 313

+   208 ND (NOT YET)

+   209 MUST NOT reply to AMRQ before knows the correct AM (OK)

+   210 MUST NOT respond to AMRQ with source address 0.0.0.0 on physical

+   211 interfaces having multiple logical i-faces with different masks

+   212 (NOT YET)

+   213 SHOULD examine all AMRQ's receives and check them (NOT YET)

+   214 SHOULD ignore invalid AMRQ's (AMSender) (NOT YET)

+   215 MUST use contents of AMRQ to determine correct AM (OK)

+   216 BROADCAST AMRQ after having configured addresses (OK -- doesn't)

+   217 MUST NOT broadcast AMRQ if not set by extract option (OK, no option)

+   218 MUST use the <NetPrefix> -1 ) form of broadcast addresses (OK)

+   219 4.3.3.1 (Router Advertisement and Solicitations)

+   220 MUST support router part of Router Discovery Protocol on all networks

+   221 support broadcast or multicast addressing. (OK -- done by gated)

+   222 MUST have config parameters with the respective defaults (OK)

# Figure 6.148 CMP, router requirement conformance: linux/ipv4/icmp.

+   223 5.2.7.1 (Destination Unreachable)

+   224 MUST GENERATE DU (OK)

+   225 SHOULD choose a best-match response code (OK)

+   226 SHOULD NOT generate Host Isolated codes (OK)

+   227 SHOULD use Communication Administrat Prohibited when administratively

+   228 filtering packets (NOT YET -- bug-to-bug compatibility) and silently

+   229 MAY include config option for not generating the above and

+   230 discard the packets inside (OK)

+   231 MUST include code option for not generating Violation and

+   232 precedence control codes are used we don't generate them at all)

+   233 MUST use Unreachable or Host. Host Unknown codes whenever other hosts

+   234 on the same network may be reachable (OK -- no unreach's at)

+   235 MUST use new form of Fragmentation Needed and Def Set messages (OK)

+   236 5.2.7.2 (Redirect)

+   237 MUST NOT generate redirects (OK)

+   238 MUST be able to generate host redirects (OK)

+   239 SHOULD be able to generate+TOS redirects (NO as we do not use TOS)

+   240 MUST have an option to use Host redirects instead of Host+TOS (OK as)

+   241 +TOS redirects are used when the

+   242 MUST generate redirects forwards to the same i-face and the

+   243 dest. is on the same subset as the src. address and to no source

+   244 routing is in. (OK)

+   245 MUST NOT follow redirects when using a routing protocol (OK)

+   246 MAY use redirects if not using a routing protocol (OK, compile-time option)

+   247 MUST comply to Host Requirements when not acting as a router (OK)

+   248 5.2.7.3 (Time Exceeded)

+   249 MUST generate Time Exceeded Code 0 when discarding packet due to TTL=0 (OK)

+   250 MAY have a per-interface option to disable generation of TE messages, but

+   251 it default to "originate" (OK -- we don't support it)