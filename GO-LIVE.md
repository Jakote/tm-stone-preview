# Go-live checklist — tmstone.co.ls

Everything that can be built before the domain exists is built and pushed. What is below is
the exact sequence for the day the domain is registered. Nothing here is optional and the
order matters.

## State today, 21 September 2026

| | |
|---|---|
| Domain | **Not registered.** `tmstone.co.ls` verified available at LSNIC — "No record found", no NS records |
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

1. **Register `tmstone.co.ls`.** I cannot do this — it takes a payment instrument and an
   account. See `DOMAIN-REGISTRATION.md` for who sells it, what it costs and what Thulo needs
   to produce.
2. **Point DNS at GitHub Pages.** Four A records on the apex:
   `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   and a CNAME on `www` → `jakote.github.io`.
3. **`git mv CNAME.pending CNAME`** and push. Then Settings → Pages → Custom domain, and
   tick **Enforce HTTPS** once the certificate issues (usually under an hour, up to 24).
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
- **No email on the domain.** Cloudflare Email Routing would give `info@tmstone.co.ls`
  forwarding to his existing inbox for R0, but that requires the domain to use Cloudflare
  nameservers, which is a choice to make at registration rather than after.
