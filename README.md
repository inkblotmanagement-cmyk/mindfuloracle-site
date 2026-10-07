# mindfuloracle.com

The company website for **Mindful Oracle LLC**, a Georgia company founded by Terrance Darnell Jackson.

It is a plain static site (HTML, CSS, and a few lines of JavaScript for the mobile menu). There is no build step, no tracking, no cookies, and no paid services. It is ready to host for free on GitHub Pages.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole site: home, What we offer, Free community tools, About, Contact |
| `styles.css` | Colors and layout (dark navy and teal with gold accents, mobile-first) |
| `main.js` | Opens and closes the menu on phones |
| `404.html` | "Page not found" page |
| `assets/` | JMGL graphic (also used as the social-share image) and the favicon |
| `CNAME` | Tells GitHub Pages the site lives at `mindfuloracle.com` |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is |
| `robots.txt`, `sitemap.xml` | Help search engines find the site |

## Preview on your computer

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Publish on GitHub Pages (free)

1. Create a repo on GitHub (for example `inkblotmanagement-cmyk/mindfuloracle-site`) and push this folder to its `main` branch.
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, pick `main` and `/ (root)`, and save.
4. Under **Custom domain**, enter `mindfuloracle.com` (the `CNAME` file already contains it) and save.
5. After DNS is set up (next section) and GitHub shows the domain as verified, tick **Enforce HTTPS**. The free certificate can take up to an hour or so to appear.

> Tip: To protect the domain from being claimed by someone else's GitHub Pages site, you can also verify it in your GitHub account under **Settings → Pages → Verified domains**. GitHub will give you a TXT record to add at GoDaddy.

## Point a GoDaddy domain at GitHub Pages

Only do this if you own `mindfuloracle.com` in your GoDaddy account.

1. Sign in at godaddy.com and open **My Products → Domains → mindfuloracle.com → DNS** (sometimes called **Manage DNS**).
2. **Remove** GoDaddy's default records for the root of the domain: any **A** record with the name `@` that points to GoDaddy's parking or "website builder" address, and any **Forwarding** set up for the domain.
3. **Add four A records**, all with the name `@`:

   | Type | Name | Value | TTL |
   | --- | --- | --- | --- |
   | A | @ | 185.199.108.153 | 1 hour (or default) |
   | A | @ | 185.199.109.153 | 1 hour (or default) |
   | A | @ | 185.199.110.153 | 1 hour (or default) |
   | A | @ | 185.199.111.153 | 1 hour (or default) |

4. **Set the `www` record** as a CNAME. If a `www` CNAME already exists (GoDaddy usually adds one pointing to `@`), edit it instead of adding a second one:

   | Type | Name | Value | TTL |
   | --- | --- | --- | --- |
   | CNAME | www | inkblotmanagement-cmyk.github.io | 1 hour (or default) |

5. Save. DNS changes usually show up within an hour but can take up to 48 hours.
6. Check from a terminal:

   ```bash
   dig +short mindfuloracle.com        # should list the four 185.199.x.153 addresses
   dig +short www.mindfuloracle.com    # should show inkblotmanagement-cmyk.github.io
   ```

7. Go back to **Settings → Pages** in the GitHub repo, wait for the green "DNS check successful," then turn on **Enforce HTTPS**.

Optional IPv6 (AAAA) records for `@`: `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`.

## Content rules

The site sticks to things that are true today:

- No claims of superintelligence alignment, "unbreakable" or "irreversible" safety, guarantees, accreditation, customers, partners, revenue, or endorsements.
- The AI Literacy Certificate is a certificate of completion, not an accredited credential.
- JMGL's numbers are published as they are, including what it still misses. Update them in `index.html` if new test results come in.

## TODO for Terrance

- [ ] **Photo:** add `assets/terrance.jpg` (square, about 600×600) and swap the placeholder in the About section (instructions are in an HTML comment in `index.html`).
- [ ] **Your own words:** replace the "Coming soon" note in the About section with a few sentences about why you started Mindful Oracle.
- [ ] **Confirm domain ownership:** make sure `mindfuloracle.com` is in your GoDaddy account before changing any DNS.
- [ ] **Certificate link:** when the AI Literacy Certificate is hosted, change the "Get access" button from email to the real sign-up page.
- [ ] **Review pricing:** add a price for the AI-Safety Review if you want it on the page instead of "pricing on request."
