# Shopify Setup Guide — X11 Creatine Landing Page

## Files in this repo

| File | Purpose |
|---|---|
| `index.html` | Standalone preview — open in any browser to see the full page |
| `shopify-template.liquid` | Drop into your Shopify theme to activate on the product |

---

## Option A — Product Template (Recommended)

This gives you native Shopify cart/checkout + real price from your admin.

### Steps

1. **Open your Shopify theme editor**
   - Shopify Admin → Online Store → Themes → (your active theme) → Edit code

2. **Create the template file**
   - In the left sidebar, find the `templates/` folder → click **Add a new template**
   - Type: `product`
   - Name: `creatine-landing`
   - This creates `templates/product.creatine-landing.liquid` (or `.json` in OS 2.0 — see note below)

3. **Paste the template content**
   - Open the new file and replace all its contents with the full contents of `shopify-template.liquid`
   - Click **Save**

4. **Assign the template to your product**
   - Shopify Admin → Products → X11 Vegan Creatine Monohydrate Gummies
   - Scroll down to **Theme template** (right sidebar)
   - Select `creatine-landing`
   - Click **Save**

5. **Preview**
   - Open your product in the storefront — you'll see the new landing page

### Online Store 2.0 note (Dawn and newer themes)

If your theme uses JSON templates (most themes after 2021), Shopify will create `product.creatine-landing.json` instead. In that case:

1. Create a new section: `sections/creatine-landing.liquid`
2. Paste the full HTML/CSS/JS from `shopify-template.liquid` into that section (wrap in `{% schema %}...{% endschema %}` block at the bottom — see below)
3. In the JSON template file, reference that section

Minimal schema block to add at the bottom of the section file:
```liquid
{% schema %}
{
  "name": "Creatine Landing",
  "settings": []
}
{% endschema %}
```

---

## Option B — Custom Page (Simpler, no native cart)

Use this if you can't access theme code, or want a quick test.

1. Shopify Admin → Online Store → Pages → Add page
2. In the content area, switch to **HTML** view (the `<>` button)
3. Paste the full contents of `index.html` (everything inside `<body>`)
4. Update the "Add to Cart" button href to point to your product's `/cart/add` URL
5. Save and preview

**Limitation:** The cart button uses a direct URL, not Shopify's native cart API. Works for simple single-variant products; use Option A for variant support.

---

## Replacing the Product Image Placeholder

In `shopify-template.liquid`, the product image auto-loads from `product.featured_image`.  
Just make sure your product in Shopify Admin has a featured image uploaded — it will appear automatically.

In `index.html`, find this comment:
```html
<!-- REPLACE: swap .product-pill with <img src="YOUR_PRODUCT_IMAGE" alt="X11 Creatine Gummies"> -->
```
Replace the `.product-pill` div with:
```html
<img src="YOUR_CDN_URL" alt="X11 Vegan Creatine Monohydrate Gummies" style="width:100%;max-width:280px;border-radius:12px;position:relative">
```

---

## Updating Prices

In `shopify-template.liquid` — prices are live from Shopify (no edits needed).

In `index.html` — search for `$34.99` and `$49.99` and update to your actual prices.

---

## Meta Ads — Matching the Landing Page

For best conversion with Meta (Facebook/Instagram) ads:
- **Ad creative hook** should match the hero headline: *"Get Stronger. Recover Faster. In 2 Strawberry Gummies."*
- Use the same pink/coral color palette in your ad creative for visual continuity
- Target the landing page URL directly (not your homepage or collection page)
- Add `?utm_source=meta&utm_medium=paid` to the URL for tracking

---

## Customization Cheat Sheet

| What to change | Where in the file |
|---|---|
| Hero headline | `<h1>` in the hero section |
| Price | `$34.99` / `$49.99` (index.html) or automatic (liquid) |
| Review count | Search `2,847` |
| Testimonials | `.rev-card` blocks in the reviews section |
| Urgency copy | `.urgency` div near the final CTA |
| Accent color | `--pink: #FF3D8B` and `--coral: #FF6B35` in `:root` |
| CTA text | Any `Add to Cart` or `Buy Now` text |
