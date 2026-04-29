# From Stuck to Started — Deployment Guide

A complete sales funnel for the digital book **From Stuck to Started** by Nate O.  
Two files. One Paystack account. Live in under five minutes.

---

## Files Included

| File | Purpose |
|---|---|
| `index.html` | Landing page — sells the book, triggers Paystack payment |
| `thank-you.html` | Download page — confirms payment, delivers the PDF instantly |
| `README.md` | This guide |

---

## How the Funnel Works

```
Visitor lands on index.html
        ↓
Clicks "Get Instant Access — ₦2,500"
        ↓
Paystack checkout opens (popup or redirect)
        ↓
Payment successful
        ↓
Paystack redirects to thank-you.html
        ↓
Buyer clicks Download → PDF saves to their device
```

---

## Step 1 — Set Up Paystack

1. Log in to your Paystack dashboard at **dashboard.paystack.com**
2. Go to **Settings → API Keys & Webhooks**
3. Copy your **Public Key** (starts with `pk_live_...`)
4. Go to **Settings → Preferences → Payment Page**
5. Set your **Redirect URL** to your thank-you page URL (you will get this after deployment in Step 2)

---

## Step 2 — Deploy to Netlify (Free, 2 Minutes)

1. Go to **netlify.com/drop** in your browser
2. Create a folder on your computer called `from-stuck-to-started`
3. Put both files inside it:
   - `index.html`
   - `thank-you.html`
4. Drag the entire folder onto the Netlify Drop page
5. Netlify gives you a live URL instantly — example: `https://cheerful-moon-abc123.netlify.app`
6. Your two page URLs will be:
   - Landing page: `https://cheerful-moon-abc123.netlify.app/index.html`
   - Download page: `https://cheerful-moon-abc123.netlify.app/thank-you.html`

> To get a cleaner URL, click **Site Settings → Change Site Name** in Netlify and rename it to something like `from-stuck-to-started`.

---

## Step 3 — Connect Paystack to Your Pages

### Option A — Paystack Payment Link (Easiest)

1. In your Paystack dashboard, go to **Payment Pages → Create Payment Page**
2. Set the amount to **₦2,500**
3. Set the redirect URL to your `thank-you.html` URL
4. Copy the payment page link (looks like `https://paystack.com/pay/your-page-name`)
5. Open `index.html` in a text editor
6. Find this line:

```javascript
const PAYSTACK_LINK = 'https://paystack.com/pay/from-stuck-to-started';
```

7. Replace the URL with your actual Paystack payment link
8. Re-upload the updated `index.html` to Netlify

### Option B — Paystack Inline Popup (More seamless)

1. Open `index.html` in a text editor
2. Find this line:

```javascript
const PAYSTACK_PUBLIC_KEY = 'pk_live_YOUR_PUBLIC_KEY_HERE';
```

3. Replace `pk_live_YOUR_PUBLIC_KEY_HERE` with your actual public key
4. Scroll down and find the `triggerPaystack()` function
5. Comment out the Option B redirect block and uncomment the Option A inline popup block
6. In your Paystack dashboard, add your site URL to the allowed origins
7. Re-upload `index.html` to Netlify

---

## Updating the WhatsApp Number

The support WhatsApp number appears on the thank-you page.  
To change it, open `thank-you.html` and find:

```html
<a href="https://wa.me/2349033179833" ...>
```

Replace `2349033179833` with your number in international format (no `+`, no spaces).  
Example: for `+234 801 234 5678` use `2348012345678`.

---

## Updating the Price

The price `₦2,500` appears in three places in `index.html`. Search for `2,500` and update all three. Also update the Paystack amount in the same file:

```javascript
const BOOK_PRICE_KOBO = 250000; // ₦2,500 in kobo
```

Paystack uses kobo (multiply naira by 100). For ₦3,000 use `300000`.

---

## About the PDF Download

The book PDF is embedded directly inside `thank-you.html` as a base64 data string. This means:

- No external file hosting needed
- The download works instantly with no broken links
- The file is fully self-contained

If you update the book PDF in the future, you will need to rebuild `thank-you.html` with the new PDF embedded.

---

## Recommended Custom Domain (Optional)

For a more professional URL like `fromstucktostarted.com`:

1. Buy the domain from **Namecheap** or **Godaddy**
2. In Netlify go to **Site Settings → Domain Management → Add Custom Domain**
3. Follow the DNS instructions Netlify provides
4. Done — your site goes live on your own domain within minutes

---

## Quick Checklist Before Going Live

- [ ] Paystack public key added to `index.html`
- [ ] Paystack payment link or inline popup configured
- [ ] Redirect URL in Paystack dashboard points to your `thank-you.html`
- [ ] Both files uploaded to Netlify
- [ ] Tested payment flow end to end (use Paystack test mode first)
- [ ] WhatsApp number is correct on `thank-you.html`

---

## Support

Built for Nate O — *From Stuck to Started*  
WhatsApp: +2349033179833
