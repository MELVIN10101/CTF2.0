# Many-Time Pad (MTP) Challenge

ACME Corporation's communications team developed a "high-performance stream cipher" for internal communications.
They claim that their implementation is mathematically unbreakable because it uses a true random key and simple XOR operations.

However, an audit of their log server revealed a critical flaw: to save computational resources, the system initializes a single session key and uses it to encrypt all messages sent during that session.

Our intercept team managed to capture a collection of hex-encoded ciphertexts from a single session.
One of these ciphertexts contains the administrator's flag.

All ciphertexts are encrypted using the same key. Can you recover the flag and decrypt the messages?

---

*Note: The intercept team also recovered a password-protected zip file (`noob_might_need_this.zip`) from the administrator's machine. It might contain a hint to help you solve the challenge.*

aaaaaNNNN
