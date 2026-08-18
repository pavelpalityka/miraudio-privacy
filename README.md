# Privacy policy site (Miraudio)

Static multilingual privacy policy for **Google Play Console** and the in-app **About → Privacy Policy** link.

## Contents

| Path | Purpose |
|------|---------|
| `index.html` | Main page |
| `styles.css` | Layout (light/dark) |
| `app.js` | Language picker + JSON loader |
| `content/en.json` | English (canonical) |
| `content/ru.json` | Russian |
| `content/uk.json` | Ukrainian |
| `content/*.json` | Other app locales (English body + localized notice) |
| `generate_content.py` | Regenerate fallback locales after editing `en.json` |

## Google Play

1. Publish this folder to a **public HTTPS URL** (see hosting below).
2. In Play Console → **App content** → **Privacy policy**, paste that URL.
3. Update the URL in `AppSettings::privacyPolicyUrl()` if it differs from the default.

Required because Miraudio uses **Appodeal** advertising mediation and **Google Play Billing**.
The policy must mention collection of **IP address** and **advertising identifier (GAID)** and link to [Appodeal’s privacy policy](https://www.appodeal.com/privacy-policy).

## app-ads.txt

Place `app-ads.txt` (this folder) at the **root of the developer website domain** listed in Google Play, for example:

`https://pavelpalityka.github.io/app-ads.txt`

Crawlers look at the domain root, not `…/miraudio-privacy/app-ads.txt`.
The file already has Appodeal account `439467`. AdMob / Meta placeholder lines are commented out until you have your own IDs.

## Hosting options

### GitHub Pages (recommended)

1. Push the repo to GitHub (e.g. `pavelpalityka/miraudio`).
2. **Settings → Pages → Build from branch** → branch `main`, folder `/docs` **or** copy `docs/privacy/` to `gh-pages` branch root.
3.    If the repo is `pavelpalityka/miraudio` and you serve `/docs`, enable Pages on `/docs` — URL becomes:
   `https://pavelpalityka.github.io/miraudio/privacy/`

   Alternatively publish only `docs/privacy/` as site root on `gh-pages` → `https://pavelpalityka.github.io/miraudio/`

4. Verify `?lang=ru` opens Russian text.

### Other hosts

Upload the whole `docs/privacy/` directory to any static host (Netlify, Cloudflare Pages, your domain).

## Local preview

From this directory:

```bash
python -m http.server 8080
```

Open `http://localhost:8080/?lang=ru`

## Updating the policy

1. Edit `content/en.json` (and `ru.json` / `uk.json` if needed).
2. Run `python generate_content.py` to refresh fallback locales.
3. Redeploy the site.
4. Change the **Last updated** date in JSON files.

## Languages

- **Full translation:** English, Russian, Ukrainian.
- **Other app languages:** English text + banner in the user’s language (legally binding version is English).

To add a full translation, add `content/xx.json` and include `xx` in `SUPPORTED_FULL` in `app.js`.

## Contact

Policy contact email: `pavelpalityka@gmail.com` (must match Play Console developer contact).
