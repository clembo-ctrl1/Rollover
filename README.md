# 🔄 Rollover Store — by One-Up

Your custom AI-powered dropshipping website, built with Next.js and connected to Shopify's Storefront API. Hosted for free on Vercel.

---

## How This Works

```
Customer visits your site → Browses products (pulled from Shopify) → Adds to cart → Checks out on Shopify
```

Your custom website handles the look and feel. Shopify handles the products, payments, and orders behind the scenes. Best of both worlds.

---

## Step-by-Step Setup (for non-technical users)

### Part 1: Get Your Shopify Storefront Token

This is DIFFERENT from the Admin API token. The Storefront token is safe to use in your website because it can only *read* products — it can't modify your store.

1. Log into your Shopify admin
2. Click **Settings** (gear icon, bottom left)
3. Click **Apps and sales channels**
4. Click **Develop apps** at the top
5. Click on your **Rollover Bot** app (or create a new one called "Rollover Website")
6. Click **Configure Storefront API scopes**
7. Check these boxes:
   - `unauthenticated_read_product_listings`
   - `unauthenticated_read_product_tags`
   - `unauthenticated_read_checkouts`
   - `unauthenticated_write_checkouts`
8. Click **Save**, then click **Install app**
9. Go to the **API credentials** tab
10. Under **Storefront API access token**, click **Reveal** and copy it

You now have your Storefront token. Save it somewhere safe.

---

### Part 2: Create a GitHub Account (if you don't have one)

1. Go to [github.com](https://github.com) and sign up (it's free)
2. Once logged in, click the **+** icon in the top right → **New repository**
3. Name it `rollover-store`
4. Make it **Private**
5. Click **Create repository**

---

### Part 3: Upload the Code to GitHub

**Option A: Using GitHub's website (easiest)**

1. On your new repository page, click **"uploading an existing file"**
2. Drag and drop ALL the files from the rollover-site folder
3. Click **"Commit changes"**

**Option B: Using the terminal (if comfortable)**

```bash
cd rollover-site
git init
git add .
git commit -m "Initial Rollover store"
git remote add origin https://github.com/YOUR-USERNAME/rollover-store.git
git branch -M main
git push -u origin main
```

---

### Part 4: Deploy to Vercel (free)

1. Go to [vercel.com](https://vercel.com) and sign up with your GitHub account
2. Click **"Add New..."** → **"Project"**
3. Find your `rollover-store` repository and click **"Import"**
4. Before clicking Deploy, click **"Environment Variables"** and add:

   | Name | Value |
   |------|-------|
   | `NEXT_PUBLIC_SHOPIFY_STORE_DOMAIN` | `your-store-name.myshopify.com` |
   | `NEXT_PUBLIC_SHOPIFY_STOREFRONT_TOKEN` | `your-storefront-token-from-part-1` |

5. Click **"Deploy"**
6. Wait 1-2 minutes — Vercel will build your site
7. You'll get a URL like `rollover-store.vercel.app` — that's your live website!

---

### Part 5: Connect Your Custom Domain (optional)

1. In Vercel, go to your project → **Settings** → **Domains**
2. Type in your domain (e.g., `rollover.one-up.cloud`)
3. Vercel will show you DNS records to add
4. Go to your domain provider (Cloudflare, etc.) and add those records
5. Wait a few minutes for DNS to propagate
6. Your custom domain is now live!

---

## Project Structure

```
rollover-site/
├── app/
│   ├── layout.js          # Site-wide layout (navbar, cart, fonts)
│   ├── page.js            # Landing page (what visitors see first)
│   ├── globals.css         # Styles and animations
│   └── shop/
│       └── page.js        # Product listing (pulls from Shopify)
├── components/
│   ├── Navbar.js          # Top navigation bar
│   ├── CartPanel.js       # Slide-out shopping cart
│   ├── CartProvider.js    # Cart state management
│   └── ProductCard.js     # Individual product display
├── lib/
│   └── shopify.js         # Shopify Storefront API client
├── .env.example           # Template for your environment variables
├── next.config.js         # Next.js configuration
├── tailwind.config.js     # Styling configuration
└── package.json           # Project dependencies
```

---

## FAQ

**Q: Do I need to add products manually?**
No — the Rollover Bot (separate project) adds products to your Shopify store automatically. This website then displays them.

**Q: Is Vercel really free?**
Yes, for personal projects. The free tier includes 100GB bandwidth/month which is plenty to start. You only pay if you get massive traffic (a good problem to have).

**Q: How do I update the design?**
Edit the files in the `app/` and `components/` folders, push to GitHub, and Vercel auto-deploys the changes.

**Q: Where do orders go?**
All orders go to your Shopify admin dashboard. When a customer clicks "Checkout" on your site, they're redirected to Shopify's secure checkout page. You manage everything in Shopify.
