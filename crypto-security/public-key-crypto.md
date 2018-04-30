# Public-key crypto & digital signature

Public-key cryptography, or asymmetrical cryptography, is any cryptographic system that uses pairs of keys: public keys which may be disseminated widely, and private keys which are known only to the owner.

The two best-known uses of public-key cryptography are:

1. **authentication (or signatures)**: a message is signed with the sender's private key and can be verified by anyone who see the sender's public key. This verification proves that the sender had access to the private key (and therefore is likely to be the person associated with the public key, i.e. the sender).
2. **public-key encryption (PKE)**: the sender encrypts his message with the recipient's **public key**. The message cannot be decrypted by anyone but the paired private key holder (who is presumed to be the person associated with the public key).

The signature also ensures that the message has not been tampered with, as a signature is mathematically bound to the message it originally was made with.


## Authentication/digital signatures
A digital signature is a mathematical scheme for presenting the authenticity of digital messages or documents through **asymmetric (or public-key) cryptography** 

A valid digital signature gives a recipient reason to believe:

1. that the message was created by a known sender (authentication)
2. that the sender cannot deny having sent the message (non-repudiation)
3. that the message was not altered in transit (integrity).

Note that **signature does not mean encryption**: everyone can verify the author, and signature does not imply anything about the secrecy of exchange data.

## Public-key encryption (PKE)

Any person can encrypt a message using the receiver's public key. That encrypted message can only be decrypted with the receiver's private key.

The strength of a PKE relies on the computational effort ("work factor") required to find the private key from its paired public key (i.e. mathematically always possible but very long).
A private key can generate many different public keys. The generation of a public key from a private key is expected to be trivial, the opposite almost impossible.

Effective security only requires keeping the private key private; the public key can be openly distributed with no effect on security.

Any mathematical problem that currently admit no efficient solution (one-way function) can be used to create a public key from a private one:

- integer factorization (as in RSA)
- discrete logarithm
- elliptic curve relationships...


## Hybrid cryptosystems

The main pro of PK algorithms over symmetric key is **convenience**: they do not require a secure channel for the initial exchange of one or more secret keys.

The main con is **slowness**: the computational complexity is much higher than of symmetric encryption (a typical symmetric encryption is about 4000 times faster than the asymmetric version). Also, a typical crypto like RSA cannot encrypt anything larger than its modulus, which is generally less than or equal 4096 bits, far smaller than the largest messages we'd like to send. Still, the most important reason is the speed argument given above.

Therefore **hybrid cryptosystems**: they combine the convenience of public-key systems with the efficiency of symmetric-key systems.

Hybrid crypto are **very** common (PGP, PKCS, TLS/SSL...): all practical implementations of public-key cryptography today employ the use of a hybrid system.


1. PK crypto is used only for the symmetric key encapsulation scheme, which handles only a small block of data (e.g. Diffie-Helmann key exchange)

2. the symmetric key is then used for the data encapsulation scheme (e.g. AES), which might be much longer. The symmetric encryption/decryption is based on simpler algorithms (block/stream ciphers) and is much faster.


### Symmetric encryption

Symmetric-key systems (also "private-key encryption") use the same keys for both encryption of plaintext and decryption of ciphertext. It's the encryption used to encrypt data on a computer, for instance (where the sender and the receiver are the same person in a different time).

Symmetric-key encryption can use either stream ciphers or block ciphers:

- **stream ciphers** encrypt the digits (typically bytes), or letters (in substitution ciphers) of a message one at a time. An example is the Vigenere Cipher.
- **block ciphers** take a number of bits and encrypt them as a single unit, padding the plaintext so that it is a multiple of the block size. Blocks of 64/128 bits are commonly used.

