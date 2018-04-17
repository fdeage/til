# DNS basics

DNS is a **distributed, coherent, reliable, autonomous, hierarchical database**, the first and only one of its kind.
DNS is both a system and a protocol.

## Structure
- 13 root nameservers only
- each server contains a copy of the same big file, refreshed and replaced twice a day (?)
- small file that acts as the Net’s definitive directory

## Naming
- the DNS namespace has a tree structure, where every node has a parent (except the root node, which is its own parent)
- FQDN (Fully Qualified Domain Name): node names, bottom up, with each followed by a period.
Ex: www.google.com is the FQDN of a node whose name is www, whose parent is google, whose grandparent is com, and whose great-grandparent is the DNS root
- nodes have labels 1-63 characters long (except root node which label is empty), total FQDN must be =< 255
- character set of a DNS label is modified US-ASCII

## DNS search order
- check if it's a FQDN, adds the final dot/beginning "http"
- check in the browser cache
- check in the `/etc/hosts` file
- ISP cache?
- ask the DNS server (order can be defined by the user)

[ACM on DNS complexity](https://queue.acm.org/detail.cfm?id=1242499)
