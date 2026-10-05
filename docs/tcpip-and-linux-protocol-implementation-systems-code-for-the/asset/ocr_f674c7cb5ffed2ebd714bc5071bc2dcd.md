# Glossary

RTT (Round-Trip Time). One of the critical performance parameters for a TCP flow.

Scale (see aggregation). QoS requires state. State incurs costs in memory and in messages to establish it. The state may simply be a constant increase over the state needed for destination routing—however, usually destinations are heavily aggregated (e.g., at least by network number, also by CIDR, and so on). Flows are per-user, may be present in much larger numbers than host IDs, although if the phone net is anything to go by, this is not true.

SCFQ. Self-Cloced Fair Queuing.

Schedule. A neat way to think about scheduling is to take a picture of a resource shared over time and picture how it is decreased by someone else asking for special circumstances.

+   1. FIFO/FCFS (in first, out first; out first, first served)—A strange but widespread service discipline in IP (and multiprotocol) routers.
2. Drop policy—Tail drop, head drop, random (set RED). When the queue is full, which packet gets lost?
3. Priority queue—When there is more than one packet in a queue, which gets forwarded? Note priority queuing can starve lower-priority packets of ever service.
4. Precedence queuing—Priority queue based on the precedence bits in the IP header.
5. Custom queuing—A (proprietary, but commonly used by other names) scheme to give certain flows a minimum performance through hardwired classifications and minimum queue service rates.
6. Fair queuing (WFQ)—Round robin.
7. Weighted Fair Queuing (WFQ)—Round robin (rounding error is to allow for variable length packets—weight in WFQ sometimes used to refer to unfair share; actually, the P in GPS—see GPS and PGPS).
8. Virtual Clock—A service scheme for TDM that still stat muxes.
9. Generalized Processor Sharing (GPS)—The theory of WFQ—fluid flow.
10. Packet Generalized Processor Sharing (PGPS)—The practice of WFQ—packet flow.
11. Earliest Due Date (EDD)—A neat alternative scheduler for delay bounding.

SE style. Shared explicit reservation style, which has explicit sender selection and shared attributes.