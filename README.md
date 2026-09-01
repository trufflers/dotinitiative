# The DOT Initiative — website

A single-page static site. No build step, no framework, no dependencies.
Everything is in `index.html` (HTML, CSS and one small script together) plus the
`images/` folder.

---

## Before you publish: photo consent

Two of the photos (`marble-ramp.jpg`, `marshmallow-tower.jpg`) show grade 3
students' faces clearly. Before this goes live, confirm with West Point Grey
Academy that those specific children have media releases covering **public
external use**, not only the school magazine. Schools treat those as different
permissions and it is the school's call, not yours.

If any consent is missing, delete that `<figure>` block from the gallery section
and the page still works — the hero photo (`building-hands.jpg`) shows hands
only and carries no identification risk.

The student quotes deliberately use first names and "grade 3" with no last
initial and no graduating year. On a public page indexed by Google, a first
name plus `'35` pins a specific eight-year-old to a specific school. Keep it
that way.

---

## Put it on GitHub Pages

1. Create a GitHub account if you don't have one.
2. Make a **new public repository**. Name it `dot-site` (any name works).
3. Upload every file in this folder, keeping the structure:
   ```
   index.html
   CNAME
   .nojekyll
   images/building-hands.jpg
   images/marble-ramp.jpg
   images/marshmallow-tower.jpg
   ```
   Use **Add file → Upload files** and drag the whole lot in. The `images`
   folder must stay a folder.
4. Go to **Settings → Pages**. Under "Build and deployment", set Source to
   *Deploy from a branch*, branch `main`, folder `/ (root)`. Save.
5. Wait a minute or two. Your site appears at
   `https://YOURUSERNAME.github.io/dot-site/`. Check it works before touching DNS.

---

## Reconnect dotinitiative.com

**Do GitHub first, DNS second.** Adding the domain at your registrar before
adding it in GitHub can let someone else claim it.

**Step 1 — tell GitHub about the domain.**
Settings → Pages → Custom domain → enter `dotinitiative.com` → Save.
(The `CNAME` file in this repo already contains that domain, so this may fill in
by itself.)

**Step 2 — remove the old Google Sites records.**
Log in to whoever you bought the domain from and open the DNS settings. Delete
any existing A, AAAA, ALIAS or CNAME records for the root domain and for `www`.
Those currently point at Google Sites and will conflict.

**Step 3 — add these records.**

For the root domain (`dotinitiative.com`) — four A records. The host/name field
is usually `@` or left blank:

| Type | Name | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

Optionally also add AAAA records for IPv6 (keep the A records either way):

| Type | Name | Value |
|------|------|-------|
| AAAA | @ | 2606:50c0:8000::153 |
| AAAA | @ | 2606:50c0:8001::153 |
| AAAA | @ | 2606:50c0:8002::153 |
| AAAA | @ | 2606:50c0:8003::153 |

For `www`, one CNAME:

| Type | Name | Value |
|------|------|-------|
| CNAME | www | YOURUSERNAME.github.io |

That value is your *account* Pages domain — no repository name on the end.

**Step 4 — wait, then turn on HTTPS.**
DNS changes can take up to 24 hours, though it is often minutes. Once GitHub
stops showing a DNS error on the Pages settings screen, tick **Enforce HTTPS**.
The certificate is free and automatic. If the tickbox is greyed out, the DNS
hasn't propagated yet — come back later.

These IP addresses are current as of writing but GitHub does change them
occasionally. If something doesn't work, check GitHub's own page for
"Managing a custom domain for your GitHub Pages site".

---

## Updating the site later

**The session counter.** Near the bottom of `index.html`:

```js
var SESSIONS = 25;
```

Change that number and the row of dots redraws — one filled dot per session,
plus one open pink circle for the next one. Update the `25+` figure and the
"Twenty-five Thursdays" sentence to match.

**Adding a school.** Copy one `<li>` in the `.schools` list and edit it. Update
the `3` in the figures strip.

**Adding photos.** Save into `images/`, then copy a `<figure>` block in the
gallery. Always write real alt text. Resize to roughly 1200px on the long edge
and export as JPEG at about 80% quality — full-size phone photos will make the
page slow on mobile data.

**New quotes.** Copy an `<li>` in the `.qlist` block. First name and grade only.

## Things worth doing next

- Get an email address on the domain (`hello@dotinitiative.com`) instead of the
  Gmail one. Most registrars sell forwarding for a few dollars a year, and it
  looks materially more credible to a sponsor.
- Add a photo from each new school as the program expands. Evidence of multiple
  sites is the single most useful thing you can add before applying for
  anything bigger.
- Keep a running count of students reached per term. Grant applications ask, and
  reconstructing it a year later is painful.
