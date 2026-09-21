# Go-live checklist — tmstone.co.ls

Everything that can be built before the domain exists is built and pushed. What is below is
the exact sequence for the day the domain is registered. Nothing here is optional and the
order matters.

## State today, 21 September 2026

| | |
|---|---|
| Domain | **Not registered.** `tmstone.co.ls` has no NS and no A record, re-checked 21 Sept. M220/year at Zeecom |
| Hosting | GitHub Pages, repo `Jakote/tm-stone-preview`, public |
| Live at | `https://jakote.github.io/tm-stone-preview/` |
| Indexed | **No, on purpose.** `noindex,nofollow` on both pages |

The preview address must never be the one Google indexes. If it is, the real domain spends
months competing against a github.io URL for its own name. That is why the noindex stays on
until the domain resolves, and why every canonical, og:url and sitemap entry already points
at `tmstone.co.ls` rather than at the address the site is actually served from today.

## Already done

- `<link rel="canonical">` → `https://tmstone.co.ls/`
- Open Graph: type, site_name, locale `en_LS`, url, title, description, image + dimensions + alt
- Twitter `summary_large_image`, `theme-color`
- `LocalBusiness` JSON-LD — legal name, registration **A2026/34518**, Ha Tsosane Pela
  Boitumela, phone, founding year 2020, area served, what he sells. Validates as JSON.
- `robots.txt` — currently `Disallow: /`, with the sitemap line already correct
- `sitemap.xml` — home page only, and says in a comment why `/quote/` is excluded
- `CNAME.pending` — holds the hostname, named so GitHub Pages ignores it until the rename

## The go-live sequence

1. **Register `tmstone.co.ls` — M220/year at Zeecom, `my.zeecom.co.ls`.** Online, card, same
   day. No Lesotho company needed, no documents, no registration number: LSNIC policy §3.1 is
   "any natural person, company or organization". At the order screen, set the nameservers to
   the **Cloudflare** pair for the new zone (create the zone in Cloudflare first, free tier, so
   you have the pair to paste). Doing it at order time means every later DNS change happens in
   Cloudflare and you never touch the registrar portal again.
   **Register it to TM Stone as registrant, MEND as technical contact only** — the registrant
   holds the transfer rights and gets the renewal notices. And agree in writing who pays the
   M220, this year and every year, before ordering. Full research in `DOMAIN-REGISTRATION.md`.
   *This is the one step I cannot do: it needs an account and a card.*

2. **In Cloudflare, add the records.** Apex `tmstone.co.ls`, four A records — these are the
   live values, re-resolved from `jakote.github.io` on 21 September, not quoted from memory:
   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```
   and `www` as a CNAME to `jakote.github.io`.
   **Set the proxy to DNS-only (grey cloud) for now.** Orange-cloud proxying in front of
   GitHub Pages breaks Pages' own certificate issuance until the cert exists.
   *Delegation to Cloudflare is proven on this TLD, not assumed — `zeecom.co.ls` and the
   regulator's own `lca.org.ls` both resolve to Cloudflare nameservers today.*

3. **`git mv CNAME.pending CNAME`** and push. Then Settings → Pages → Custom domain →
   `tmstone.co.ls`, and tick **Enforce HTTPS** once the certificate issues (usually under an
   hour, up to 24).

4. **Verify the certificate and the redirect** before touching anything else. `https://tmstone.co.ls`
   must load with a valid certificate and `www` must land on the apex.
5. **Only then, open the index.** Delete the `noindex,nofollow` line in `index.html` (it is
   marked `DELETE AT GO-LIVE`) and replace `robots.txt` with:
   ```
   User-agent: *
   Allow: /
   Disallow: /quote/

   Sitemap: https://tmstone.co.ls/sitemap.xml
   ```
6. **Submit the sitemap** in Google Search Console, after verifying the domain there by DNS
   TXT record. Bing Webmaster Tools imports from Search Console in one click.
7. **Google Business Profile.** This matters more than the website for a Maseru trade
   business — it is what puts him on the map pin when someone searches "paving Maseru". It
   needs postcard or phone verification at the Ha Tsosane address and only Thulo can do it.

## Left deliberately undone

- **`/quote/` stays `noindex` and out of the sitemap.** It is a price calculator and its
  numbers are still unconfirmed — the two calculators disagree on batch yield (432 vs 480),
  which is one of the four questions sent to Thulo on 21 September. Publishing his prices to
  Google before he has confirmed them, and before he has said he wants them public at all, is
  his decision and not mine.
- **No email on the domain yet.** Once the zone is on Cloudflare, Email Routing gives
  `info@tmstone.co.ls` forwarding into his existing inbox for R0 — two MX records and a TXT,
  added in the same dashboard. Worth doing the same day, because an email address on his own
  domain is the cheapest credibility a trade business can buy. It is a separate step and it
  needs his say-so on which inbox it forwards to.
