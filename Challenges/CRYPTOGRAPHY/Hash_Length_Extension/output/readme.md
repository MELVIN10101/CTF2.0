# Aegis Core API Gateway - Authentication Bypass

During a network security assessment of Aegis Core's infrastructure, we intercepted a signed API request granting guest console access.

- **Target API endpoint**: `/***/*******`
- **Guest query payload**: `user=guest&auth=false`
- **MAC Signature (Hex)**: (See the generated `challenge.txt`)
- **Key details**: The secret key is a random ASCII string of unknown length, but we know it lies in the range of 16 to 32 bytes.

The gateway verifies the integrity of the request using a custom MAC scheme:
$$\text{MAC}(\text{payload}) = \text{SHA256}(\text{secret\_key} \parallel \text{payload})$$

If the signature matches and the parsed query string parameter `auth` evaluates to `true`, the gateway grants full administrative console access.

Because the gateway processes parameters sequentially, submitting a query string containing duplicate keys like:
`user=guest&auth=false...&auth=true`
will cause the query string parser to resolve the value of `auth` to `true` (taking the last parameter).

---

## Challenge Objective

Use a **Hash Length Extension** attack to append `&auth=true` to the guest query parameters and compute a valid signature for the extended payload. 

Since the length of the secret key is unknown, you will need to:
1. Try different possible secret key lengths (from 16 to 32 bytes).
2. For each key length, compute the MD-padding for the original message.
3. Append the extension payload (`&auth=true`).
4. Perform the state resume SHA-256 calculation to generate the extended signature.
5. Send the extended query string (with URL-encoded binary padding) and signature to `/api/console`.

Good luck!
