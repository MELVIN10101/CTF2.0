# HTTP Request Smuggling (CL.XCL Desync)

Welcome to the CorpNet Internal Portal Assessment.

## Background
The internal portal is hosted behind an Nginx frontend reverse proxy and a custom Python HTTP/1.1 socket server backend. Traffic is proxied over a persistent HTTP/1.1 connection.

A security audit suggests the backend server parses custom headers inconsistently compared to the frontend. In particular, check how the server reads content lengths when both `Content-Length` and a custom `X-Content-Length` header are present in a single pipeline stream.

## Objective
Your goal is to perform an HTTP Request Smuggling (CL.XCL desynchronization) attack.
1. Intercept requests to the portal at `http://web10.ctf/` 
2. Identify the desynchronization behavior when sending both `Content-Length` and `X-Content-Length`.
3. Smuggle a request payload that bypasses Nginx's proxy restrictions to access `/admin/flag` and retrieve the flag.

## Connection Specs
- **Frontend Portal**: `http://web10.ctf/`
- **Forbidden Endpoint**: `http://web10.ctf/admin/flag`  (blocked directly at proxy layer, return 403)

Good luck!
