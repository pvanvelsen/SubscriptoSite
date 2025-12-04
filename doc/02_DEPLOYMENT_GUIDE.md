# Subscripto Website - Deployment Guide

**Created:** December 4, 2024
**Status:** Ready for Deployment

---

## ✅ What's Been Built

Your Subscripto static website is **complete and ready to deploy**!

### Pages Implemented

1. **Home Page** (`/`)
   - "Coming Soon" message with Subscripto branding
   - Logo with green "o" matching app design
   - Coming soon badge
   - Tagline and description
   - Hidden App Store/Play Store buttons (ready to unhide)
   - Footer with privacy policy link

2. **Privacy Policy** (`/privacy`)
   - Comprehensive GDPR/CCPA compliant policy
   - Covers all Subscripto features and data practices
   - Mobile-responsive with print-friendly styles
   - Markdown-based for easy updates

3. **Email Verification** (`/verify`)
   - Handles Supabase authentication redirects
   - Success and error states
   - Deep link to open mobile app
   - Auto-redirect on mobile devices
   - Fallback to download page

### Features Included

- ✅ Material 3 design matching mobile app
- ✅ Light and dark mode support
- ✅ Responsive design (mobile-first)
- ✅ SEO optimized (meta tags, sitemap)
- ✅ Fast loading (minimal JavaScript)
- ✅ GitHub Pages deployment workflow
- ✅ Custom domain ready (subscripto.io)

---

## 🚀 Deployment Steps

### Step 1: Create GitHub Repository

```bash
# If you haven't already pushed to GitHub:

# 1. Create a new repository on GitHub named "SubscriptoSite"
#    (or any name you prefer)

# 2. Add GitHub remote
git remote add origin https://github.com/YOUR_USERNAME/SubscriptoSite.git

# 3. Push to GitHub
git push -u origin main
```

### Step 2: Configure GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** → **Pages** (left sidebar)
3. Under "Build and deployment":
   - **Source:** Select "GitHub Actions"
4. The site will build automatically when you push to `main`

### Step 3: Configure Custom Domain

#### In GitHub Repository

1. Still in **Settings** → **Pages**
2. Under "Custom domain":
   - Enter: `subscripto.io`
   - Click **Save**
3. Wait for DNS check to complete
4. Enable **Enforce HTTPS** (after DNS propagates)

#### In Your Domain Registrar

Configure the following DNS records for `subscripto.io`:

**For Apex Domain (subscripto.io):**
```
Type: A
Host: @
Value: 185.199.108.153

Type: A
Host: @
Value: 185.199.109.153

Type: A
Host: @
Value: 185.199.110.153

Type: A
Host: @
Value: 185.199.111.153
```

**For IPv6 (optional but recommended):**
```
Type: AAAA
Host: @
Value: 2606:50c0:8000::153

Type: AAAA
Host: @
Value: 2606:50c0:8001::153

Type: AAAA
Host: @
Value: 2606:50c0:8002::153

Type: AAAA
Host: @
Value: 2606:50c0:8003::153
```

**DNS Propagation:** Can take 5 minutes to 48 hours (usually < 1 hour)

### Step 4: Configure Supabase

1. Go to your Supabase project dashboard
2. Navigate to **Authentication** → **URL Configuration**
3. Set the following:

```yaml
Site URL: https://subscripto.io
Redirect URLs:
  - https://subscripto.io/verify
  - http://localhost:4321/verify  # For local testing
```

4. Update email templates if needed:
   - Go to **Authentication** → **Email Templates**
   - Ensure "Confirm signup" template uses `{{ .ConfirmationURL }}`

### Step 5: Verify Deployment

After GitHub Actions completes and DNS propagates:

1. Visit `https://subscripto.io`
   - Should show the coming soon page
   - Logo should display with green "o"
   - Dark mode should work

2. Visit `https://subscripto.io/privacy`
   - Privacy policy should render correctly
   - All sections should be readable

3. Visit `https://subscripto.io/verify?token=test`
   - Should show error state (invalid token)
   - Confirms page is working

4. Test Supabase flow:
   - Create a test user in your app
   - Check email verification link
   - Should redirect to `https://subscripto.io/verify?token=...`
   - Should show success message

---

## 🔧 Post-Deployment Tasks

### Enable App Store Buttons

When ready to launch the mobile app:

1. Edit `src/pages/index.astro`
2. Find the line: `<div class="app-links hidden space-y-4 md:space-y-0 md:space-x-4">`
3. Remove the `hidden` class
4. Update the `href="#"` values to actual App Store URLs
5. Commit and push to deploy

### Update Privacy Policy

To update the privacy policy:

1. Edit `src/content/privacy.md` (plain markdown)
2. Update the "Last Updated" date
3. Commit and push - GitHub Actions will rebuild automatically

---

## 📊 Monitoring

### Check Deployment Status

- GitHub Actions: `https://github.com/YOUR_USERNAME/SubscriptoSite/actions`
- Every push to `main` triggers automatic deployment
- Build takes ~2-3 minutes

### Verify HTTPS Certificate

- Visit `https://subscripto.io`
- Check for green padlock in browser
- Certificate should be valid for both:
  - `subscripto.io`
  - `www.subscripto.io` (if configured)

---

## 🐛 Troubleshooting

### Site Not Loading

**Issue:** `404 Not Found` after deployment

**Solutions:**
1. Check GitHub Actions completed successfully
2. Verify CNAME file exists in `dist/` folder after build
3. Ensure GitHub Pages is set to "GitHub Actions" source
4. Wait 5-10 minutes after initial setup

---

### Custom Domain Not Working

**Issue:** `subscripto.io` shows "Site not found"

**Solutions:**
1. Verify DNS records are correct (use `dig subscripto.io`)
2. Wait for DNS propagation (up to 48 hours)
3. Check CNAME file contains only: `subscripto.io` (no https://)
4. Disable and re-enable custom domain in GitHub Settings

---

### HTTPS Not Available

**Issue:** "Not secure" warning in browser

**Solutions:**
1. Wait for DNS to fully propagate first
2. Then enable "Enforce HTTPS" in GitHub Pages settings
3. GitHub will provision certificate automatically (takes 10-30 minutes)
4. Clear browser cache and try again

---

### Supabase Redirect Fails

**Issue:** Email verification doesn't redirect properly

**Solutions:**
1. Check Supabase redirect URLs include `/verify` path
2. Verify URL is HTTPS (not HTTP)
3. Test with: `https://subscripto.io/verify?token=test&type=signup`
4. Should show error page (confirms routing works)

---

## 🔄 Making Updates

### To Update Content

```bash
# 1. Make changes to files
# 2. Test locally
npm run dev

# 3. Build and test production
npm run build
npm run preview

# 4. Commit and push
git add .
git commit -m "Update: description of changes"
git push

# 5. GitHub Actions deploys automatically (2-3 minutes)
```

### To Add New Pages

1. Create `src/pages/yourpage.astro`
2. Use `BaseLayout` component
3. Add navigation link if needed
4. Commit and push

Example:
```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
---

<BaseLayout title="Your Page">
  <h1>Content here</h1>
</BaseLayout>
```

---

## 📝 Next Steps (Future)

When ready to expand the site:

### Phase 2: Content Pages
- `/features` - Feature showcase
- `/faq` - Frequently asked questions
- `/blog` - Blog for SEO

### Phase 3: Interactive Features
- Email signup form (for launch notifications)
- Subscription calculator
- Demo video

### Phase 4: Analytics
- Add privacy-friendly analytics (Plausible, Simple Analytics)
- Track conversion metrics
- Monitor page performance

---

## 🎉 You're Done!

Your Subscripto website is ready to go live. Just:

1. Push to GitHub
2. Configure DNS
3. Wait for deployment
4. Configure Supabase

The site will be live at `https://subscripto.io` within an hour!

---

## 📞 Support

**Questions?**
- Check GitHub Actions logs for build errors
- Review Astro docs: https://docs.astro.build
- GitHub Pages docs: https://docs.github.com/en/pages

**Contact:**
- Email: peter@subscripto.io
- Project docs: `doc/01_INITIAL_DEVELOPMENT.md`

---

**Deployment Guide v1.0**
**Created:** December 4, 2024
