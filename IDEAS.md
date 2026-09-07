# Workshop Ideas

## Sensitive values in mirrored headers

- Mark a fake canary credential with `x-mcp-header`.
- Show that it appears in both the request body and an `Mcp-Param-*` header.
- Demonstrate how proxies, WAFs, tracing, or debug logs may capture custom headers.
- Explain that Base64 is transport encoding, not encryption, and custom headers may miss standard credential-redaction rules.

## MRTR request state

- Put a fake key in Base64-encoded `requestState` to show that opaque does not mean secret.
- Compare unsigned state, HMAC-signed state, and AEAD-protected state.
- Emphasize principal binding, short expiry, original-request binding, and server-side single-use enforcement where required.
- Key message: **opaque is not secret, signed is not encrypted, and encrypted is not replay-proof**.

## Elicitation boundary

- Show an intentionally non-compliant form-mode request for a fake API key.
- Contrast it with URL-mode elicitation, where the credential does not pass through the MCP client or LLM.
- Use only clearly fake, scoped workshop credentials and benign logging as the observable outcome.
