# aw-oidc

Public OIDC discovery for an agent-warrant SPIRE trust domain, so Anthropic's
workload identity federation can verify the model gateway's JWT-SVIDs while SPIRE
itself stays off the internet.

- `.well-known/openid-configuration`: the discovery document (issuer
  `https://smangs.github.io/aw-oidc`).
- `keys.json`: SPIRE's JWT signing keys (public keys only), exported with
  `spire-server bundle show -format spiffe`, keeping the `jwt-svid` keys.

Update `keys.json` whenever SPIRE rotates its JWT keys: add a new key as soon as
it appears in SPIRE's bundle (at least 15 minutes before SPIRE signs with it), and
remove a key once it has left the bundle.
