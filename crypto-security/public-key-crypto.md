# Public-key crypto & digital signature

Public-key cryptography, or asymmetrical cryptography, is any cryptographic system that uses pairs of keys: public keys which may be disseminated widely, and private keys which are known only to the owner.

The two best-known uses of public-key cryptography are:

1. **authentication (or signatures)**: a message is signed with the sender's private key and can be verified by anyone who see the sender's public key. This verification proves that the sender had access to the private key (and therefore is likely to be the person associated with the public key, i.e. the sender).
2. **public-key encryption**: the sender encrypts his message with the recipient's **public key**. The message cannot be decrypted by anyone but the paired private key holder (who is presumed to be the person associated with the public key).

The signature also ensures that the message has not been tampered with, as a signature is mathematically bound to the message it originally was made with.


## Authentication/digital signatures
A digital signature is a mathematical scheme for presenting the authenticity of digital messages or documents through **asymmetric (or public-key) cryptography** 

A valid digital signature gives a recipient reason to believe:

1. that the message was created by a known sender (authentication)
2. that the sender cannot deny having sent the message (non-repudiation)
3. that the message was not altered in transit (integrity).

Note that **signature does not mean encryption**: everyone can verify the author, and signature does not imply anything about the secrecy of exchange data.

## Public-key encryption

Any person can encrypt a message using the receiver's public key. That encrypted message can only be decrypted with the receiver's private key.

The strength of a public key cryptography system relies on the computational effort ("work factor") required to find the private key from its paired public key (mathematically possible but very long).
A private key can generate many different public keys. The generation of a public key from a private key is expected to be trivial.

Effective security only requires keeping the private key private; the public key can be openly distributed without compromising security.

Any mathematical problem that currently admit no efficient solution (one-way function) can be used:

- integer factorization (e.g. in RSA)
- discrete logarithm
- elliptic curve relationships...


## Hybrid cryptosystems

The main pro of PK algorithms over symmetric key is **convenience**: they do not require a secure channel for the initial exchange of one or more secret keys.

The main con is **slowness**: the computational complexity is much higher than of symmetric encryption.

Therefore **hybrid cryptosystems**: they combine the convenience of public-key systems with the efficiency of symmetric-key systems. 

Hybrid crypto are **very** common (PGP, PKCS, TLS/SSL...): all practical implementations of public-key cryptography today employ the use of a hybrid system. 


1. PK crypto is used only for the symmetric key encapsulation scheme, which handles only a small block of data (e.g. Diffie-Helmann key exchange)

2. the symmetric key is then used for the data encapsulation scheme (e.g. AES), which might be much longerThe symmetric encryption/decryption is based on simpler algorithms (block/stream ciphers) and is much faster.


Symmetric key systems use the same keys for both encryption of plaintext and decryption of ciphertext.

