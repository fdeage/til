# `/dev/random` vs `/dev/urandom`

Both are random devices that produce uniformly distributed random byte values of potentially high quality.

Man page: "On Linux, `/dev/urandom` will produce lower quality output if the entropy pool drains, while `/dev/random` will prefer to block and wait for additional entropy to be collected."

But there is currently no knowledge of how to exploit the "lower quality" of `urandom`. Every serious cryptographer uses `urandom`.

Sane behaviour: blocking random until the kernel has gathered enough initial entropy, and never blocking after that point.
FreeBSD does it, while Linux's `/dev/urandom` happily gives you not-so-random numbers before the kernel even had the chance to gather entropy (at system start, booting the computer).

## On macOS
On macOS, the random device implements the Yarrow cryptographically secure pseudo-random number generator (CSPRNG) algorithm and maintains its entropy pool, so that both are equivalent. The kernel automatically seeds the algorithm with additional entropy during normal execution.

The Yarrow algorithm is used for FreeBSD, and was inherited by Mac OS X. On both of these operating systems, it's used to implement `/dev/random`. Unlike on Linux, `/dev/urandom` is just an alias for `/dev/random`.

cf. [Myths about urandom](https://www.2uo.de/myths-about-urandom/)
