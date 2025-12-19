# The Snake Pit - Stripe Subscription Setup Guide

## Files Created
- `snake-pit-subscription.html` - Main landing page
- `success.html` - Post-purchase confirmation page

## Setup Steps

### 1. Get Your Stripe API Keys

Action → Go to Stripe Dashboard
Command → Visit https://dashboard.stripe.com/test/apikeys
Expected result → See "Publishable key" (starts with pk_test_)

**Copy the Publishable key** - You'll paste this in step 3.

⚠️ Use test mode keys first. Switch to live mode after testing.

---

### 2. Create Subscription Product in Stripe

Action → Create product in Stripe Dashboard
Command → Go to https://dashboard.stripe.com/test/products

Steps:
1. Click "Add product"
2. Enter details:
   - Name: "Monthly Membership"
   - Description: "The Snake Pit - Mixed Martial Arts & Fitness"
3. Under Pricing:
   - Price: £40
   - Billing period: Monthly
   - Currency: GBP
4. Click "Save product"

Expected result → Product created with a Price ID (starts with price_)

**Copy the Price ID** - You'll paste this in step 3.

---

### 3. Configure the Landing Page

Action → Edit snake-pit-subscription.html
Command → Open in text editor and replace two values:

Find line 130:
```javascript
const stripe = Stripe('YOUR_STRIPE_PUBLISHABLE_KEY');
```
Replace with:
```javascript
const stripe = Stripe('pk_test_YOUR_ACTUAL_KEY_HERE');
```

Find line 133:
```javascript
const priceId = 'YOUR_PRICE_ID';
```
Replace with:
```javascript
const priceId = 'price_YOUR_ACTUAL_ID_HERE';
```

Expected result → File configured with your Stripe credentials

---

### 4. Host the Files

**Option A - GitHub Pages (Free, easiest)**

Action → Create GitHub repository
Command → 
1. Create new repo at github.com/new
2. Upload both HTML files
3. Go to Settings > Pages
4. Select main branch as source
5. Save

Expected result → Live URL like `https://yourusername.github.io/reponame`

**Option B - Netlify (Free, drag-and-drop)**

Action → Deploy to Netlify
Command → 
1. Go to netlify.com
2. Drag folder with both HTML files
3. Site deploys automatically

Expected result → Live URL like `https://random-name.netlify.app`

**Option C - Your hosting**

Upload both files to your web server. Ensure success.html is in the same directory as the main page.

---

### 5. Test the Subscription

Action → Test in Stripe test mode
Command → 
1. Visit your hosted landing page
2. Click "Subscribe Now"
3. Use test card: 4242 4242 4242 4242
4. Any future expiry date
5. Any CVC

Expected result → Redirects to success page, subscription appears in Stripe Dashboard

⚠️ Test mode payments won't charge real money.

---

### 6. Go Live

Action → Switch to production keys
Command → 
1. Toggle Stripe Dashboard to "Live mode"
2. Copy live Publishable key (starts with pk_live_)
3. Copy live Price ID from your product
4. Replace keys in the HTML file
5. Re-upload to hosting

Expected result → Landing page accepts real payments

---

## Quality Checks

✓ Landing page loads without errors
✓ "Subscribe Now" button works
✓ Stripe Checkout opens with correct price (£40/month)
✓ Success page displays after test purchase
✓ Subscription appears in Stripe Dashboard
✓ Customer receives confirmation email

---

## Common Issues

**"Invalid API key"**
Cause → Wrong key format or not copied fully
Fix → Verify key starts with pk_test_ or pk_live_

**"No such price"**
Cause → Price ID doesn't exist or wrong mode (test vs live)
Fix → Verify Price ID in Stripe Dashboard matches file

**Success page 404**
Cause → success.html not uploaded or wrong path
Fix → Ensure success.html is in same directory as main page

---

## Customization Options

**Change description:**
Edit line 113 in snake-pit-subscription.html

**Change colors:**
Edit CSS in `<style>` section (lines 8-99)

**Add logo:**
Insert before `<h1>` tag:
```html
<img src="your-logo.png" alt="The Snake Pit" style="width: 150px; margin-bottom: 20px;">
```

---

## Next Steps After Setup

1. Share landing page URL with potential members
2. Monitor subscriptions in Stripe Dashboard
3. Set up webhook for automated member management (optional, advanced)
4. Configure email notifications in Stripe settings

Time to complete: 30-45 minutes including Stripe account setup
