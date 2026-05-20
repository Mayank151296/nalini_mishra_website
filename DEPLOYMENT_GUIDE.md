# nalinimishra.in — Deployment Guide
## GitHub + Cloudflare Pages + GoDaddy DNS

---

## STEP 1 — Push to GitHub

1. Go to https://github.com/new
2. Repository name: `nalini-mishra-website`
3. Set to **Public** → **Create repository** (don't tick "Add README")

Then open **Terminal** on your Mac and run these one at a time:

```bash
cd /Users/mayankjoshi/Desktop/nalini_mishra_website
git init
git add .
git commit -m "Initial commit — nalinimishra.in"
git branch -M main
git remote add origin https://github.com/Mayank151296/nalini-mishra-website.git
git push -u origin main
```

> When prompted for password, paste your **GitHub Personal Access Token** (not your password).
> Generate one at: https://github.com/settings/tokens/new — tick `repo` scope.
> The token won't show as you type — just paste and hit Enter.

---

## STEP 2 — Deploy on Cloudflare Pages

1. Go to https://dash.cloudflare.com
2. **Workers & Pages** → **Create application** → **Pages** → **Connect to Git**
3. Authorise GitHub if prompted → select `nalini-mishra-website`
4. Build settings:
   - **Framework preset**: `None`
   - **Build command**: *(leave blank)*
   - **Build output directory**: *(leave blank)*
5. Click **Save and Deploy** — site goes live at `nalini-mishra-website.pages.dev` in ~60 sec

---

## STEP 3 — Connect domain `nalinimishra.in` (GoDaddy → Cloudflare)

### A. Add the domain to Cloudflare (one-time)

1. In Cloudflare dashboard → **Add a Site** → enter `nalinimishra.in` → choose **Free plan**
2. Cloudflare scans existing DNS records (just click Continue)
3. **Cloudflare gives you 2 nameservers** — they look like:
   - `xxx.ns.cloudflare.com`
   - `yyy.ns.cloudflare.com`
   Keep this tab open.

### B. Point GoDaddy to Cloudflare

1. Login to **GoDaddy** → **My Products** → find `nalinimishra.in` → **DNS**
2. Scroll to **Nameservers** → click **Change** → **Enter my own nameservers**
3. Paste the two Cloudflare nameservers from Step 3A → **Save**
4. Wait 10–60 min (sometimes faster) for propagation. Track at **dnschecker.org**.

### C. Add custom domain to Pages project

1. Back in Cloudflare → **Workers & Pages** → click `nalini-mishra-website` project
2. **Custom domains** tab → **Set up a custom domain**
3. Enter `nalinimishra.in` → Continue → it auto-creates a CNAME record. Done.
4. Repeat for `www.nalinimishra.in` (recommended).
5. SSL auto-provisions in 1–5 min.

---

## STEP 4 — Verify

Visit:
- https://nalinimishra.in
- https://www.nalinimishra.in

Both should load with a green padlock (HTTPS).

---

## To update the site later

```bash
cd /Users/mayankjoshi/Desktop/nalini_mishra_website
# (make edits to index.html or images)
git add .
git commit -m "Update content"
git push
```

Cloudflare Pages auto-deploys within 60 seconds of every push to `main`.

---

## File structure

```
nalini_mishra_website/
├── index.html                    # The one-pager
├── DEPLOYMENT_GUIDE.md           # This file
├── images/
│   ├── omnr-logo.png             # Brand logo (nav + footer)
│   ├── ostwal-imperial-hero.jpeg # Ostwal hero
│   ├── ostwal-imperial-card.jpeg # Portfolio tile
│   ├── ostwal-aerial.jpeg        # Gallery
│   ├── ostwal-night.jpeg
│   ├── ostwal-garden.jpeg
│   ├── ostwal-elevation-day.jpeg
│   ├── ostwal-impression.jpeg
│   ├── image_010 → 014.jpeg      # Shree Balaji Pride gallery
│   └── image_016 → 020.jpeg      # Shiv Srushti gallery
├── brochures/
│   ├── ostwal-imperial.pdf
│   ├── shree-balaji-pride.pdf
│   └── shiv-shrushti.pdf
└── qr/
    └── ostwal-imperial-mrera-qr.png
```

---

## Quick troubleshooting

- **GoDaddy doesn't let me change nameservers**: usually because domain is locked. Unlock under **Domain Settings → Domain Lock**.
- **Pages says "domain already exists"**: someone else might have added it on Cloudflare. Use Cloudflare support chat to release it.
- **SSL pending**: takes up to 24 hrs in rare cases. Just wait.
- **Old GoDaddy email forwarding stops working**: nameserver change moves DNS to Cloudflare, so any GoDaddy-managed email needs new MX records added in Cloudflare.

---

## Contact info hardcoded on site

- Phone / WhatsApp: **+91 82628 85023**
- Email: **sales@nalinimishra.in** (you'll need to set this up via your email provider after domain is live)
- Address: **Plot No. 13, Jay Gurudev Bunglow, Vajali Pada, Devisha Road, Palghar West — 401404**

If any of these need to change, edit them inline in `index.html` — search & replace `82628 85023`, `sales@nalinimishra.in`, etc.
