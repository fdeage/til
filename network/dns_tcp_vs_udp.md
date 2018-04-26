# DNS: TCP vs UDP

- UDP is connexion-less: the nameserver doesn’t keep track of any form of “connexion” (like TCP does with handshake)
- it’s faster since there is no handshake (which means only 1 round-trip vs at least 2 in TCP)
- If it fails, the user has to re-request the resolution (= reliability lies on the app side)
- if payload > 512 bytes, there will be at least 2 packets: since reliability also includes order, the user has to use TCP
- TCP can be forced by the user (even for 1 packet), but some DNS servers won’t accept TCP because of a higher DOS risk
- some DNS extensions allow larger packets (e.g. for emails, recognized by most MTU)
- standard DNS port is 53, secure DNS (over TLS) is 853 ([RFC 7858](https://tools.ietf.org/html/rfc7858))

## Links

[ACM on DNS complexity](https://queue.acm.org/detail.cfm?id=1242499)