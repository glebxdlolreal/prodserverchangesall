# prodserverchangesall

Automated snapshot repository for **Telegram production server** resources. A background worker periodically fetches pages and files from the production server, strips volatile data, and commits changes here — building a full history of production web resource changes.

The equivalent repository for the **test** server: [testserverchangesall](https://github.com/glebxdlolreal/testserverchangesall)

---


## Content normalization

Before comparison and saving, the following volatile data is stripped so commits reflect only real changes:

- `<time>` tags
- Query params: `?hash=`, `?token=`, `passport_ssid=`, `nonce`
- Versioned cache-buster suffixes on JS/CSS (e.g. `?12345_67890`)
- HTML comments like `<!-- page generated in N ms -->`
- IP addresses in the format `X.X.X.X:8888`
- Signature fields `sig=` and `se=` in config strings

`help.getAppConfig.json` is compared with noisy fields excluded (`hash`, `ton_usd_rate`), so only meaningful config changes trigger a commit.

---

## Related repositories

| Repository | Description |
|---|---|
| [testserverchangesall](https://github.com/glebxdlolreal/testserverchangesall) | Test server snapshots |
