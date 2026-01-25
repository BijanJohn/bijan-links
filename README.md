# Bijan Links

A simple linktree-style landing page to replace the GoHighLevel hosted version.

## Project Files

- `index.html` - Main landing page
- `style.css` - Styling
- `profile.jpg` - Profile image (add your own)

## Setup Checklist

### Phase 1: Domain Transfer (In Progress)

- [x] Initiate domain transfer from GoHighLevel to Cloudflare
- [x] Cloudflare account configured and ready
- [ ] GHL support processes transfer
- [ ] Approve transfer via email confirmation
- [ ] Wait 5-7 days for transfer to complete
- [ ] Verify domain is active in Cloudflare

### Phase 2: Email Setup (After Transfer Completes)

#### Step 1: Upgrade Tuta Account
- [ ] Log into [tutamail.com](https://tutamail.com)
- [ ] Go to Settings > Subscription
- [ ] Upgrade to **Revolutionary** plan (~$3/month)

#### Step 2: Add Custom Domain in Tuta
- [ ] Go to Settings > Email > Custom email domains
- [ ] Click "Add custom domain"
- [ ] Enter `bijantech.com`
- [ ] Note down the DNS records Tuta provides

#### Step 3: Configure DNS in Cloudflare
- [ ] Log into [dash.cloudflare.com](https://dash.cloudflare.com)
- [ ] Select `bijantech.com`
- [ ] Go to DNS > Records
- [ ] **Remove** old Mailgun MX records
- [ ] **Add** the following records:

**MX Record:**
```
Type: MX
Name: @
Mail server: mail.tutanota.de
Priority: 10
Proxy status: DNS only
```

**SPF Record:**
```
Type: TXT
Name: @
Content: v=spf1 include:spf.tutanota.de -all
```

**DKIM Record:**
```
Type: TXT
Name: s1._domainkey
Content: (copy from Tuta dashboard)
```

**DMARC Record (recommended):**
```
Type: TXT
Name: _dmarc
Content: v=DMARC1; p=quarantine;
```

#### Step 4: Verify Domain in Tuta
- [ ] Return to Tuta custom domain settings
- [ ] Click "Verify" or refresh
- [ ] Wait for green checkmarks on all records (may take up to 24 hours)

#### Step 5: Create Email Address
- [ ] In Tuta, go to Settings > Email > Email aliases
- [ ] Create your preferred address (e.g., `hello@bijantech.com`, `bijan@bijantech.com`)

### Phase 3: Linktree Hosting

#### Option A: GitHub Pages
- [ ] Push this repo to GitHub
- [ ] Go to repo Settings > Pages
- [ ] Set source to "Deploy from a branch" > `main`
- [ ] Note the URL: `https://yourusername.github.io/bijan-links`

#### Option B: Custom Subdomain (e.g., links.bijantech.com)
- [ ] Deploy to GitHub Pages, Netlify, or Vercel
- [ ] In Cloudflare DNS, add:
```
Type: CNAME
Name: links
Target: yourusername.github.io (or netlify/vercel URL)
Proxy status: Proxied
```

#### Option C: Root Domain (bijantech.com)
- [ ] Deploy to hosting provider
- [ ] In Cloudflare DNS, add A or CNAME record pointing to host
- [ ] Consider what happens to existing bijantech.com content

### Phase 4: Update Links

- [x] Set up Substack blog (https://substack.com/@bijanyoga)
- [x] Update blog URL in `index.html`
- [ ] Add profile image (`profile.jpg`)
- [ ] Test all links work correctly

---

## Quick Reference

**Cloudflare Dashboard:** https://dash.cloudflare.com

**Tuta Dashboard:** https://app.tuta.com

**Domain:** bijantech.com

**Email Provider:** Tuta (Revolutionary plan)

---

## Notes

- Email DNS changes may take up to 24-48 hours to fully propagate
- During email switchover, there may be a brief gap in receiving emails
- Keep old MX records until Tuta is verified and working
