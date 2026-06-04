# VoltDiagnostics - Side-Channel Evaluation

Welcome to the VoltDiagnostics side-channel audit portal.

Your objective is to evaluate a secure cryptographic hardware module implementing AES-128 with a first-order Boolean masking countermeasure. The designers claim that first-order masking prevents any key recovery because all intermediate variables are randomized by independent masks:
$$X_{\text{masked}} = X \oplus M$$
$$\text{SBox}_{\text{masked}} = \text{SBox}(P \oplus K) \oplus M$$

However, a first-order masking countermeasure is vulnerable to a **second-order Correlation Power Analysis (CPA)** attack. By correlating the combination of two leakage points—one leaking the mask $M_j$, and one leaking the masked S-box output $\text{SBox}(P_j \oplus K_j) \oplus M_j$—you can bypass the masking defense and recover the secret key byte $K_j$.

We have captured power consumption traces during the Round 1 SubBytes execution for 5,000 encryptions. The leakage points for the mask and S-box output are at unknown, fixed cycle indices in the trace.

---

## Provided Files

1. `traces.bin`: A raw binary file containing 5,000 traces of 120 samples each.
   - **Format**: Flat array of 32-bit floats (`float32`), total size: 2,400,000 bytes.
   - **Shape**: (5000, 120)
2. `plaintexts.bin`: A raw binary file containing the 5,000 corresponding plaintexts (16 bytes each).
   - **Format**: Flat array of unsigned bytes (`uint8`), total size: 80,000 bytes.
   - **Shape**: (5000, 16)
3. `challenge.txt`: Contains the hexadecimal string values for the AES-128-GCM encrypted flag:
   - `ciphertext`
   - `nonce`
   - `tag`

---

## Challenge Objective

Recover the secret 16-byte AES-128 key by executing a second-order CPA attack. Once recovered, decrypt the flag in `challenge.txt` using AES-128-GCM with the recovered key.

Good luck!
