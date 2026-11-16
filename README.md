# prodserverchangesall

Automated snapshot repository for **Telegram production server** resources: web pages, static files, and selected Telegram API responses. Changes are normalized and committed here to preserve their history.

The equivalent repository for the **test** server: [testserverchangesall](https://github.com/glebxdlolreal/testserverchangesall)

---

## Repository structure

Web resources (HTML, JS, CSS, images, and related files) are stored at the repository root. Telegram API snapshots use `<namespace>.<method>.json` filenames alongside them.

---

## Telegram API snapshots

Selected responses cover application and server configuration, countries and time zones, Premium information, theme backdrops, interest categories, transcription models, wallet rates and provider information. A snapshot appears when the corresponding method is available on the server.

`aicompose.getTones.json` contains only system AI compose styles. User-created styles and their authors are excluded.

---

## Content normalization

Before comparison and saving, the following volatile data is stripped so commits reflect only real changes:

- `<time>` tags
- Query params: `?hash=`, `?token=`, `passport_ssid=`, `nonce`
- Versioned cache-buster suffixes on JS/CSS (e.g. `?12345_67890`)
- HTML comments like `<!-- page generated in N ms -->`
- IP addresses in the format `X.X.X.X:8888`
- Signature fields `sig=` and `se=` in config strings

`help.getAppConfig.json` is compared with noisy fields excluded (`hash`, `ton_usd_rate`), so only meaningful config changes trigger a commit. Other API snapshots also filter volatile fields and account-specific data before saving.

---

## Related repositories

| Repository | Description |
|---|---|
| [testserverchangesall](https://github.com/glebxdlolreal/testserverchangesall) | Test server snapshots |
