# DNS basics

DNS is a **distributed, coherent, reliable, autonomous, hierarchical database**, the first and only one of its kind.
DNS is both a system and a protocol.

## Structure
- 13 root nameservers only
- each server contains a copy of the same big file, refreshed and replaced twice a day (?)
- small file that acts as the Net’s definitive directory 

## Naming
- the DNS namespace has a tree structure, where every node has a parent (except the root node, which is its own parent)
- nodes have labels 1-63 characters long (except root node which label is empty)
- FQDN (Fully Qualified Domain Name): node names, bottom up, with each followed by a period.
Ex: ww.google.com is the FQDN of a node whose name is www, whose parent is google, whose grandparent is com, and whose great-grandparent is the DNS root
- character set of a DNS label is modified US-ASCII

## UDP/TCP protocols
- UCP is connexion-less: the nameserver doesn’t keep track of any form of “connexion”
- it’s faster since there is no handshake (which means only 1 round-trip instead of at least 2 in TCP)
- If it fails, the user has to re-request the resolution (= reliability lies on the app side)
- if payload > 512 bytes, there will be at least 2 packets: since reliability also includes order, the protocol HAS to be TCP
- TCP can be forced by the user (even for 1 packet), but some DNS servers won’t accept TCP because of a higher DOS risk
- some DNS extensions allow larger packets (for emails, recognized by most MTU)
- standard DNS port is 53

## Links

[ACM on DNS complexity](https://queue.acm.org/detail.cfm?id=1242499)