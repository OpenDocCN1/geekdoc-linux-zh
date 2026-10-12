# 8.7 Delegation – iterative and recursive queries; subdomains

For convenience we have repeated here the diagram and tcpdump trace from Module 8.5.

# Iterative and recursive queries

In Module 8.5 we said there was no difference in format between queries sent from a client to a DNS server, and from one DNS server to another. However, Figure 8.11 suggests there is a difference. When our DNS server received the query (step 3 in the diagram) it sent off several queries (4, 6, 8) until it had resolved the question completely. However, when the other servers in the diagram received a query, they resolved only one component of the query and immediately returned the answer.

![](bbox=[0.25, 0.3, 0.83, 0.68])

Figure 8.11 The full DNS conversation to resolve www.ibm.com

What’s happening is that DNS allows two types of queries, which are distinguished by setting a special flag on or off in the packet.

+   1. recursive: the requestor (which could be the resolver in our client, or our DNS server when it’s talking to the other servers) says “please resolve this query completely; you should carry out all the intermediate steps to process delegations, and just give me the final answer.” The query (3) from the resolver in our client is recursive
+   2. iterative: the requestor expects the server to perform only the first step of the resolving. If further steps are needed, the requestor uses the information in the reply to issue the next request, etc. Queries (4 and 8) from the server are iterative.