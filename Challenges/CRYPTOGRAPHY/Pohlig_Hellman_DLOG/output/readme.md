# Smooth Operator

Our threat intelligence unit has intercepted an encrypted payload transmission from a secure military communication network. 
The system administrators recently updated their encryption scheme, transitioning to a custom key-exchange system. They claim that by using a composite modulus $N = p \cdot q$ of 2048 bits instead of a standard prime field, they have made the discrete logarithm problem completely intractable, even to quantum computers (a typical marketing claim).

However, during a code audit of their key generation module, we discovered that they generated the primes $p$ and $q$ using a custom random number generator. The generator was configured with a specific optimization designed to speed up exponentiation by ensuring the prime factors of $p-1$ and $q-1$ are "highly structured."

Our analysis indicates that this optimization makes $p-1$ and $q-1$ extremely smooth.

Can you bypass their defenses, factor the modulus, solve the discrete logarithm problem, and decrypt the flag?

The intercept team recovered the public parameters and the encrypted payload, which are stored in `challenge.txt`.
The AES-256-GCM decryption key for the flag is the SHA-256 hash of the raw bytes of the discrete log $x$ (in big-endian format).

*"When a path is made too smooth, the traveler might slide right through the gate."*
