# Palm Cafe – Hostinger Deployment Guide

## What You Have
- `index.html` — the complete website (single file, no server needed)

---

## Step-by-Step: Deploy to Hostinger

### Step 1 – Log in to Hostinger
Go to → https://hpanel.hostinger.com and log in with your account.

### Step 2 – Go to File Manager
In your hosting dashboard:
1. Click **"Websites"** → select your domain
2. Click **"File Manager"** in the left menu

### Step 3 – Upload the file
1. Open the **`public_html`** folder (this is your website root)
2. Delete any existing `index.html` if present
3. Click **"Upload"** (top toolbar)
4. Upload **`index.html`** from your computer

### Step 4 – Done! ✅
Visit your domain — the Palm Cafe website is live!

---

## If You Have a Custom Domain (e.g. palmcafe.in)
1. In Hostinger hPanel → **Domains** → point your domain to your hosting
2. It may take up to 24 hours to propagate (usually under 1 hour)

---

## Add Your Logo Image (Optional Upgrade)
If you want to use the actual PNG logo instead of the SVG logo:
1. Upload `logo.png` to `public_html/` alongside `index.html`
2. In `index.html`, find the `<svg class="logo-svg"` tag in the navbar
3. Replace the entire `<svg>` with: `<img src="logo.png" alt="Palm Cafe" class="logo-svg">`

---

## Update Swiggy / Zomato Links (when listed)
1. Open the website in your browser
2. Click the **⚙️ button** (bottom-left)
3. Password: `palmcafe2024`
4. Go to **Settings tab**
5. Paste your Swiggy / Zomato restaurant URL
6. Click **Save All Settings**

> Note: Settings are saved in the visitor's browser. For permanent updates, edit the `store.swiggyLink` default in the JS section of `index.html`.

---

## Admin Panel Reference
| Setting | Default |
|---------|---------|
| Password | palmcafe2024 |
| WhatsApp | 918925962259 |
| Address | No 17, Kovalan Street... |

---

## SSL Certificate (HTTPS) – Free on Hostinger
1. hPanel → **SSL** → **Install SSL**
2. Select your domain → Click **Install**
3. Your site will be secure at `https://yourdomain.com`

---

## Support
For Hostinger help: https://support.hostinger.com
