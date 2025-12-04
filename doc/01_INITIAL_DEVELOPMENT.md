# Subscripto Static Site - Initial Development Plan

**Version:** 1.0
**Created:** December 4, 2024
**Project:** Subscripto Static Website
**Domain:** subscripto.io
**Purpose:** Landing page, privacy policy, email verification for Subscripto app

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Branding Analysis](#branding-analysis)
3. [Technical Architecture](#technical-architecture)
4. [Site Structure](#site-structure)
5. [Page Specifications](#page-specifications)
6. [Implementation Details](#implementation-details)
7. [GitHub Pages Deployment](#github-pages-deployment)
8. [Supabase Integration](#supabase-integration)
9. [Future Roadmap](#future-roadmap)
10. [Next Steps](#next-steps)

---

## Project Overview

### Purpose

Create a static website for Subscripto (family subscription tracking mobile app) with three core pages:

1. **Home Page** (`/`) - "Coming Soon" landing page with app branding
2. **Privacy Policy** (`/privacy`) - Comprehensive privacy policy for app store compliance
3. **Email Verification** (`/verify`) - Redirect target for Supabase email authentication

### Requirements

- **Hosting:** GitHub Pages (free, custom domain support)
- **Branding:** Match Subscripto mobile app (Material 3 design)
- **Extensibility:** Framework-based for future growth
- **Responsive:** Mobile-first design
- **No Analytics:** Privacy-focused (no tracking for now)
- **Hidden App Links:** App Store/Play Store buttons ready but hidden

---

## Branding Analysis

### App Branding Research

**Source:** `/Users/petervanvelsen/SubscriptoProjects/SubscriptoApp`

#### Logo Design

**Implementation:** `HomeScreen.kt:543-556`

The Subscripto logo uses multi-colored text:
- **"Subscript"** - Blue text (uses theme primary color)
- **"o"** - Green text (`#4CAF50` - Material Green 500)

```kotlin
Text(
    text = buildAnnotatedString {
        withStyle(style = SpanStyle(color = MaterialTheme.colorScheme.onPrimary)) {
            append("Subscript")
        }
        withStyle(style = SpanStyle(color = Color(0xFF4CAF50))) {
            append("o")
        }
    },
    style = MaterialTheme.typography.titleLarge,
    fontWeight = FontWeight.Bold,
    fontSize = 22.sp
)
```

**Key Colors:**
- **Brand Green:** `#4CAF50` (Material Green 500)
- **Typography:** Material 3 titleLarge, 22sp, Bold

---

### Color Palette (Material 3)

**Source:** `SubscriptoColorScheme.kt`

#### Light Mode

| Color Role | Hex Code | Purpose |
|------------|----------|---------|
| **primary** | `#1976D2` | Material Blue 700 - Trust, stability, toolbar background |
| **primaryVariant** | `#004BA0` | Material Blue 900 - Darker blue variant |
| **primaryContainer** | `#D4E6F6` | Light blue backgrounds |
| **onPrimaryContainer** | `#0D47A1` | Text on blue containers |
| **secondary** | `#4CAF50` | **Material Green 500 - The green "o" color** |
| **accent** | `#81C784` | Material Green 300 - Lighter green accent |
| **background** | `#FAFAFA` | Off-white - Main background (reduces eye strain) |
| **surface** | `#FFFFFF` | White - Card/surface backgrounds |
| **error** | `#D32F2F` | Material Red 700 - Error states |
| **onPrimary** | `#FFFFFF` | White - Text on blue primary |
| **onSecondary** | `#000000` | Black - Text on green secondary |
| **onBackground** | `#1C1B1F` | Dark gray - Text on main background |
| **onSurface** | `#1C1B1F` | Dark gray - Text on surfaces |
| **onError** | `#FFFFFF` | White - Text on error backgrounds |

#### Dark Mode

| Color Role | Hex Code | Purpose |
|------------|----------|---------|
| **primary** | `#90CAF9` | Material Blue 200 - Vibrant for dark background |
| **primaryVariant** | `#64B5F6` | Material Blue 300 - Lighter blue variant |
| **primaryContainer** | `#1A4D7A` | Dark blue container |
| **onPrimaryContainer** | `#BBDEFB` | Light blue - Text on dark containers |
| **secondary** | `#66BB6A` | Material Green 400 - Richer green for dark mode |
| **accent** | `#81C784` | Material Green 300 - Green accent |
| **background** | `#0F0F0F` | Near black - True dark background |
| **surface** | `#1C1C1E` | Dark gray - Better contrast with background |
| **error** | `#CF6679` | Material 3 dark error - Softer error color |
| **onPrimary** | `#003258` | Dark blue - Less harsh than black |
| **onSecondary** | `#003A00` | Dark green - Text on green |
| **onBackground** | `#E6E1E5` | Warm gray - Better readability |
| **onSurface** | `#E6E1E5` | Warm gray - Matches onBackground |
| **onError** | `#370B1E` | Dark red - Text on error |

---

### Typography

**Source:** `SubscriptoTheme.kt`

Uses **Material 3 default Typography** system with custom weights:

- **displayMedium** - Hero numbers (32sp, Bold) - Monthly totals
- **titleLarge** - App name, major headings (22sp, Bold)
- **titleMedium** - Section headers (16sp)
- **bodyLarge** - Error messages
- **bodyMedium** - Subscription prices (15sp, Medium)
- **bodySmall** - Context text (12-13sp)
- **labelSmall** - Category badges, timestamps (9-11sp)
- **labelMedium** - Section labels (12sp, Medium)
- **headlineSmall** - Empty state headlines (Bold)

**Font Families:**
- **iOS/macOS:** San Francisco (system default)
- **Android:** Roboto (system default)
- **Web:** System font stack (`-apple-system`, `BlinkMacSystemFont`, `Roboto`)

---

### Logo Assets

**Available Resources:**

#### Compose Multiplatform:
- `/composeApp/src/commonMain/composeResources/drawable/ic_logo_regular.png` (292KB)
- `/composeApp/src/commonMain/composeResources/drawable/ic_logo_landscape.png` (178KB)

#### Android:
- `/composeApp/src/androidMain/res/drawable/ic_splash_logo.png` (178KB)
- Launcher icons in `res/mipmap-*` (multiple densities)

#### iOS:
- `/iosApp/iosApp/Assets.xcassets/AppIcon.appiconset/app-icon-1024.png`
- `/iosApp/iosApp/Assets.xcassets/SplashLogo.imageset/splash_logo.png`

---

## Technical Architecture

### Framework Selection: Astro

**Chosen Framework:** [Astro 4.x](https://astro.build)

#### Rationale

| Requirement | How Astro Solves It |
|-------------|---------------------|
| **GitHub Pages** | Native static site generation, perfect deployment |
| **Extensibility** | Component-based, easy to scale to blog/features pages |
| **Performance** | Zero JS by default, ships minimal bundles |
| **SEO** | Built-in sitemap, meta tags, RSS support |
| **Markdown** | Native support for privacy policy content |
| **Future-Proof** | Can migrate to SSR or add React/Vue components later |

#### Why Not Alternatives?

- **Vanilla HTML/CSS:** Less maintainable, harder to scale
- **Next.js/Nuxt:** Over-engineered, harder GitHub Pages deployment
- **Vite:** Manual routing/SEO setup, less opinionated structure

---

### Tech Stack

```yaml
Framework: Astro 4.x
Styling: Tailwind CSS (Material 3-inspired custom config)
Fonts: System fonts (San Francisco, Roboto)
Icons: Lucide Icons (lightweight, tree-shakeable)
Deployment: GitHub Pages via GitHub Actions
Build Output: Static HTML/CSS/JS
Package Manager: npm
Node Version: 20.x LTS
```

---

## Site Structure

### Directory Layout

```
subscripto-site/
├── src/
│   ├── pages/
│   │   ├── index.astro           # Home (coming soon)
│   │   ├── privacy.astro         # Privacy policy
│   │   └── verify.astro          # Email verification
│   ├── components/
│   │   ├── Logo.astro            # "Subscripto" with green "o"
│   │   ├── Header.astro          # Site header
│   │   ├── Footer.astro          # Footer with privacy link
│   │   └── ThemeToggle.astro     # Light/dark mode toggle (future)
│   ├── layouts/
│   │   └── BaseLayout.astro      # Base HTML layout
│   ├── styles/
│   │   └── global.css            # Global styles + Tailwind
│   └── content/
│       └── privacy.md            # Privacy policy markdown
├── public/
│   ├── CNAME                     # subscripto.io
│   ├── favicon.ico
│   ├── logo.png                  # From app assets
│   ├── app-store-badge.svg       # Hidden for now
│   ├── google-play-badge.svg     # Hidden for now
│   └── robots.txt
├── doc/
│   └── 01_INITIAL_DEVELOPMENT.md # This file
├── .github/
│   └── workflows/
│       └── deploy.yml            # GitHub Pages deployment
├── astro.config.mjs              # Astro configuration
├── tailwind.config.mjs           # Tailwind + Material 3 colors
├── package.json
├── .gitignore
└── README.md
```

---

## Page Specifications

### 1. Home Page (`/`)

**File:** `src/pages/index.astro`

#### Purpose
"Coming Soon" landing page with Subscripto branding

#### Content Sections

1. **Hero Section**
   - **Logo:** "Subscripto" with green "o" (large, centered)
   - **Tagline:** "Family subscription tracking made simple"
   - **Coming Soon Badge:** Prominent indicator
   - **Description:** 1-2 sentence value proposition

2. **App Store Buttons** (Hidden)
   ```html
   <div class="app-links hidden">
     <a href="#" aria-label="Download on App Store">
       <img src="/app-store-badge.svg" alt="Download on the App Store">
     </a>
     <a href="#" aria-label="Get it on Google Play">
       <img src="/google-play-badge.svg" alt="Get it on Google Play">
     </a>
   </div>
   ```
   **Note:** Add `display: none;` in CSS, remove when ready to launch

3. **Footer**
   - Link to privacy policy
   - Copyright notice
   - Contact email (hello@subscripto.io)

#### Design Requirements

- **Mobile-first:** Optimized for phone screens
- **Centered layout:** Hero content vertically/horizontally centered
- **Light/dark mode:** Respects system preference (`prefers-color-scheme`)
- **Colors:** Material 3 palette from app
- **Typography:** Clean, readable system fonts
- **Animation:** Subtle fade-in on load (optional)

---

### 2. Privacy Policy (`/privacy`)

**File:** `src/pages/privacy.astro`

#### Purpose
Comprehensive privacy policy for app store compliance and user transparency

#### Implementation

**Content Source:** `src/content/privacy.md` (Markdown file)

**Features:**
- Markdown rendering via Astro Content Collections
- Auto-generated table of contents
- Last updated date from frontmatter
- Print-friendly styles
- Anchor links for each section

#### Privacy Policy Structure

**Frontmatter:**
```yaml
---
title: "Privacy Policy"
lastUpdated: "2024-12-04"
version: "1.0"
---
```

**Content Sections:**

1. **Introduction**
   - Overview of Subscripto's privacy commitment
   - Scope of policy

2. **Information We Collect**
   - Subscription data (name, cost, renewal dates, categories)
   - Household member info (names, avatars, colors)
   - Optional email (only if email scanning enabled via OAuth)
   - Device push tokens (for renewal notifications)
   - Usage data (which family members use which subscriptions)

3. **How We Use Your Data**
   - Sync subscription data across family devices
   - Send push notifications for upcoming renewals
   - Calculate household spending insights
   - Detect duplicate subscriptions
   - Provide usage analytics

4. **Data Storage & Security**
   - Hosted on Supabase (PostgreSQL, encrypted at rest)
   - Data transmitted via HTTPS (encrypted in transit)
   - Row-level security policies
   - Regular backups
   - No sale or sharing of personal data with third parties

5. **Family & Household Sharing**
   - Data shared only within your household
   - Household admins can invite/remove members
   - Members can view shared subscriptions
   - Each member controls their own profile

6. **Email Scanning Privacy** (Optional Feature)
   - OAuth 2.0 only (no password storage)
   - Read-only Gmail/Outlook access
   - Only scans for subscription receipts
   - Can revoke access anytime via Google/Microsoft account settings
   - Emails never stored on our servers

7. **Your Rights**
   - Delete account and all associated data
   - Export data (CSV format)
   - Opt-out of push notifications
   - Update or correct personal information
   - Contact privacy@subscripto.io for concerns

8. **Children's Privacy**
   - App not intended for children under 13
   - Parental consent required for minors (13-17)
   - Compliance with COPPA

9. **Third-Party Services**
   - **Supabase:** Database, authentication, real-time sync
   - **Apple Push Notification Service (APNs):** iOS notifications
   - **Firebase Cloud Messaging (FCM):** Android notifications
   - Links to third-party privacy policies

10. **Data Retention**
    - Active accounts: Data retained indefinitely
    - Deleted accounts: Data purged within 30 days
    - Backups: Deleted within 90 days

11. **International Users**
    - Data stored in US (Supabase AWS region)
    - Compliance with GDPR (EU users)
    - Privacy Shield framework

12. **Changes to Policy**
    - Notification via email or in-app message
    - Last updated date at top of policy
    - Version history

13. **Contact Information**
    - Email: privacy@subscripto.io
    - Website: https://subscripto.io
    - Response time: Within 7 business days

#### Design Requirements

- **Readable typography:** 16-18px font size, 1.6-1.8 line height
- **Clear hierarchy:** H2 for sections, H3 for subsections
- **Table of contents:** Sticky sidebar (desktop) or top (mobile)
- **Anchor links:** Each section has `id` for direct linking
- **Print styles:** Clean, paginated layout for printing
- **Responsive:** Mobile-optimized for reading on phones
- **Accessibility:** Proper heading structure, ARIA labels

---

### 3. Email Verification Success (`/verify`)

**File:** `src/pages/verify.astro`

#### Purpose
Redirect target for Supabase email authentication flow

#### URL Structure

**Base URL:** `https://subscripto.io/verify`

**Query Parameters** (from Supabase):
- `token` - Verification token (hex string)
- `type` - Verification type (e.g., `signup`, `email_change`)
- `error` - Error message (if verification failed)
- `error_description` - Detailed error description

**Example:**
```
https://subscripto.io/verify?token=abc123...&type=signup
https://subscripto.io/verify?error=invalid_token&error_description=Token%20expired
```

#### User Flow

**Success State:**
1. User clicks verification link in email
2. Supabase redirects to `/verify?token=...&type=...`
3. Page displays success message
4. Deep link button attempts to open app (`subscripto://verify`)
5. Fallback: Link to download app if not installed

**Error State:**
1. User clicks expired/invalid verification link
2. Supabase redirects to `/verify?error=...&error_description=...`
3. Page displays error message
4. Link to return home or request new verification email

#### Implementation

**Success Content:**
```html
<div class="success-state">
  <div class="icon">✓</div>
  <h1>Email Verified!</h1>
  <p>Your email has been successfully confirmed.</p>
  <button onclick="openApp()">Open Subscripto App</button>
  <p class="secondary">
    App not installed?
    <a href="/">Download here</a>
  </p>
</div>
```

**Error Content:**
```html
<div class="error-state">
  <div class="icon">⚠️</div>
  <h1>Verification Failed</h1>
  <p>{{ error_description || "Something went wrong. Please try again." }}</p>
  <a href="/" class="button">Return to Home</a>
</div>
```

**JavaScript Logic:**
```javascript
// Auto-open app on mobile (after 3 seconds)
if (isSuccess && isMobile()) {
  setTimeout(() => {
    window.location = 'subscripto://verify?token=' + token;
    // Fallback to app store after 2 seconds if app doesn't open
    setTimeout(() => {
      if (document.visibilityState === 'visible') {
        window.location = getAppStoreLink();
      }
    }, 2000);
  }, 3000);
}
```

#### Deep Link Scheme

**iOS:** `subscripto://verify`
**Android:** `subscripto://verify`

**Universal Links** (future):
- iOS: `https://subscripto.io/verify` with Associated Domains
- Android: `https://subscripto.io/verify` with App Links

#### Design Requirements

- **Simple, focused:** Single call-to-action
- **Mobile-optimized:** Large tap targets for buttons
- **Clear states:** Distinct success vs. error visual treatment
- **Brand consistency:** Use Subscripto colors and logo
- **Accessibility:** Clear error messages, keyboard navigation

---

## Implementation Details

### Logo Component

**File:** `src/components/Logo.astro`

```astro
---
interface Props {
  size?: 'small' | 'medium' | 'large';
}

const { size = 'large' } = Astro.props;

const sizeClasses = {
  small: 'text-2xl',
  medium: 'text-3xl',
  large: 'text-4xl md:text-5xl',
};
---

<h1 class={`font-bold ${sizeClasses[size]}`}>
  <span class="text-primary dark:text-primary-dark">Subscript</span><span class="text-secondary dark:text-secondary-dark">o</span>
</h1>

<style>
  /* Optional: Add text shadow for better readability */
  h1 {
    letter-spacing: -0.02em;
  }
</style>
```

**Usage:**
```astro
<Logo size="large" />   <!-- Home page -->
<Logo size="medium" />  <!-- Header -->
<Logo size="small" />   <!-- Footer -->
```

**Result:** "Subscript<span style="color: #4CAF50">o</span>"

---

### Tailwind Configuration

**File:** `tailwind.config.mjs`

```javascript
/** @type {import('tailwindcss').Config} */
export default {
  content: ['./src/**/*.{astro,html,js,jsx,md,mdx,svelte,ts,tsx,vue}'],
  darkMode: 'media', // Respects system preference
  theme: {
    extend: {
      colors: {
        // Light mode
        primary: '#1976D2',
        'primary-variant': '#004BA0',
        'primary-container': '#D4E6F6',
        secondary: '#4CAF50',
        accent: '#81C784',
        background: '#FAFAFA',
        surface: '#FFFFFF',
        error: '#D32F2F',
        'on-primary': '#FFFFFF',
        'on-background': '#1C1B1F',
        'on-surface': '#1C1B1F',

        // Dark mode
        'primary-dark': '#90CAF9',
        'primary-variant-dark': '#64B5F6',
        'primary-container-dark': '#1A4D7A',
        'secondary-dark': '#66BB6A',
        'accent-dark': '#81C784',
        'background-dark': '#0F0F0F',
        'surface-dark': '#1C1C1E',
        'error-dark': '#CF6679',
        'on-primary-dark': '#003258',
        'on-background-dark': '#E6E1E5',
        'on-surface-dark': '#E6E1E5',
      },
      fontFamily: {
        sans: [
          '-apple-system',
          'BlinkMacSystemFont',
          'Segoe UI',
          'Roboto',
          'Helvetica Neue',
          'Arial',
          'sans-serif',
        ],
      },
      fontSize: {
        'display-medium': ['2rem', { lineHeight: '1.2', fontWeight: '700' }],
        'title-large': ['1.375rem', { lineHeight: '1.3', fontWeight: '700' }],
        'title-medium': ['1rem', { lineHeight: '1.4', fontWeight: '500' }],
      },
    },
  },
  plugins: [],
};
```

---

### Base Layout

**File:** `src/layouts/BaseLayout.astro`

```astro
---
interface Props {
  title: string;
  description?: string;
  ogImage?: string;
}

const {
  title,
  description = 'Family subscription tracking made simple',
  ogImage = '/og-image.png'
} = Astro.props;

const canonicalURL = new URL(Astro.url.pathname, Astro.site);
---

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="icon" type="image/x-icon" href="/favicon.ico" />
    <link rel="canonical" href={canonicalURL} />

    <!-- Primary Meta Tags -->
    <title>{title} | Subscripto</title>
    <meta name="title" content={`${title} | Subscripto`} />
    <meta name="description" content={description} />

    <!-- Open Graph / Facebook -->
    <meta property="og:type" content="website" />
    <meta property="og:url" content={canonicalURL} />
    <meta property="og:title" content={`${title} | Subscripto`} />
    <meta property="og:description" content={description} />
    <meta property="og:image" content={ogImage} />

    <!-- Twitter -->
    <meta property="twitter:card" content="summary_large_image" />
    <meta property="twitter:url" content={canonicalURL} />
    <meta property="twitter:title" content={`${title} | Subscripto`} />
    <meta property="twitter:description" content={description} />
    <meta property="twitter:image" content={ogImage} />

    <!-- Theme Color -->
    <meta name="theme-color" content="#1976D2" media="(prefers-color-scheme: light)" />
    <meta name="theme-color" content="#90CAF9" media="(prefers-color-scheme: dark)" />

    <!-- Generator -->
    <meta name="generator" content={Astro.generator} />
  </head>

  <body class="bg-background dark:bg-background-dark text-on-background dark:text-on-background-dark">
    <slot />
  </body>
</html>

<style is:global>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  html {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  body {
    min-height: 100vh;
  }
</style>
```

---

### Global Styles

**File:** `src/styles/global.css`

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

/* Custom utilities */
@layer utilities {
  .hidden {
    display: none !important;
  }
}

/* Material 3-inspired elevation shadows */
@layer components {
  .elevation-1 {
    box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
  }

  .elevation-2 {
    box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
  }

  .elevation-3 {
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  }
}

/* Print styles for privacy policy */
@media print {
  body {
    background: white;
    color: black;
  }

  nav, footer, .no-print {
    display: none;
  }

  a {
    text-decoration: underline;
  }

  a[href]:after {
    content: " (" attr(href) ")";
  }
}
```

---

## GitHub Pages Deployment

### Astro Configuration

**File:** `astro.config.mjs`

```javascript
import { defineConfig } from 'astro/config';
import tailwind from '@astrojs/tailwind';

// https://astro.build/config
export default defineConfig({
  site: 'https://subscripto.io',
  integrations: [tailwind()],
  build: {
    assets: '_astro',
  },
});
```

---

### GitHub Actions Workflow

**File:** `.github/workflows/deploy.yml`

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Build site
        run: npm run build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: ./dist

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

---

### Custom Domain Setup

#### 1. CNAME File

**File:** `public/CNAME`

```
subscripto.io
```

#### 2. DNS Configuration

Configure DNS at your domain registrar:

**Option A: Apex Domain (subscripto.io)**
```
A     @     185.199.108.153
A     @     185.199.109.153
A     @     185.199.110.153
A     @     185.199.111.153
AAAA  @     2606:50c0:8000::153
AAAA  @     2606:50c0:8001::153
AAAA  @     2606:50c0:8002::153
AAAA  @     2606:50c0:8003::153
```

**Option B: CNAME (if using www subdomain)**
```
CNAME www   yourusername.github.io
```

#### 3. GitHub Repository Settings

1. Go to **Settings → Pages**
2. Set **Source** to "GitHub Actions"
3. Set **Custom domain** to `subscripto.io`
4. Enable **Enforce HTTPS** (wait for SSL provisioning, ~10 minutes)

---

### Robots.txt

**File:** `public/robots.txt`

```
# Allow all crawlers
User-agent: *
Allow: /

# Sitemap
Sitemap: https://subscripto.io/sitemap-index.xml
```

**Note:** Astro auto-generates sitemap at build time.

---

## Supabase Integration

### Email Authentication Redirect

#### 1. Supabase Dashboard Configuration

**Navigate to:** Authentication → URL Configuration

**Settings:**
```yaml
Site URL: https://subscripto.io
Redirect URLs:
  - https://subscripto.io/verify
  - https://localhost:3000/verify  # For local testing
```

#### 2. Email Templates

**Template:** Confirm signup

**Subject:** `Confirm Your Email - Subscripto`

**Body:**
```html
<h2>Welcome to Subscripto!</h2>

<p>Thanks for signing up. Please confirm your email address by clicking the button below:</p>

<a href="{{ .ConfirmationURL }}" style="display: inline-block; padding: 12px 24px; background-color: #1976D2; color: white; text-decoration: none; border-radius: 4px;">
  Confirm Email
</a>

<p style="color: #666; font-size: 14px; margin-top: 20px;">
  If you didn't create this account, you can safely ignore this email.
</p>

<p style="color: #666; font-size: 14px;">
  Or copy and paste this link into your browser:<br>
  {{ .ConfirmationURL }}
</p>
```

**Note:** `{{ .ConfirmationURL }}` automatically includes the token and redirects to your configured URL.

#### 3. Deep Link Configuration

**iOS Universal Links** (Future):
- Add Associated Domains entitlement
- Create `apple-app-site-association` file
- Place in `public/.well-known/`

**Android App Links** (Future):
- Add intent filter in AndroidManifest.xml
- Create `assetlinks.json` file
- Place in `public/.well-known/`

**Current Implementation:** Uses custom URL scheme (`subscripto://`)

---

## Future Roadmap

### Phase 2: Content Expansion

**Target:** Post-MVP (after app launch)

**New Pages:**
- `/features` - Feature showcase with screenshots
- `/pricing` - Pricing tiers (when monetization launches)
- `/faq` - Frequently asked questions
- `/blog` - Blog for SEO and user education

**Content Collections:**
```
src/content/
├── blog/
│   ├── 2024-12-15-launch-announcement.md
│   └── 2025-01-10-family-budgeting-tips.md
├── features/
│   ├── subscription-tracking.md
│   └── family-sharing.md
└── faq/
    └── general.md
```

---

### Phase 3: Interactive Features

**Target:** 3-6 months post-launch

**Features:**
- **Subscription Calculator:** Interactive tool to estimate savings
- **Demo Video:** Embedded product demo
- **Testimonials Section:** User reviews and stories
- **Press Kit:** Media assets for journalists
- **Waitlist Form:** Email capture for beta features

**Technical Additions:**
- Form handling (Netlify Forms or Formspree)
- Email marketing integration (ConvertKit, Mailchimp)
- Analytics (Plausible or Simple Analytics)

---

### Phase 4: Advanced Capabilities

**Target:** 6-12 months post-launch

**Migration to Astro SSR:**
- Server-side rendering for dynamic content
- User accounts/dashboards (if needed)
- API integration with Subscripto backend

**Community Features:**
- Forum or discussion board
- User-submitted subscription database
- Community-sourced pricing data

**Monetization:**
- Affiliate links to subscription services
- Sponsored content (ethical, transparent)
- Premium content for paid users

---

## Next Steps

### Immediate Actions

1. **Initialize Project**
   ```bash
   npm create astro@latest subscripto-site
   cd subscripto-site
   npm install -D tailwindcss @astrojs/tailwind
   npx astro add tailwind
   ```

2. **Extract Logo Assets**
   - Copy `ic_logo_regular.png` from app project
   - Optimize for web (convert to WebP, create favicon)

3. **Build Core Pages**
   - Implement `index.astro` (coming soon page)
   - Implement `privacy.astro` (privacy policy)
   - Implement `verify.astro` (email verification)
   - Create `Logo.astro` component

4. **Write Privacy Policy**
   - Draft comprehensive `privacy.md` content
   - Ensure app store compliance (Apple, Google)

5. **Configure Deployment**
   - Set up GitHub Actions workflow
   - Add `CNAME` file
   - Test deployment to GitHub Pages

6. **Test & Validate**
   - Test on iOS Safari, Android Chrome
   - Validate HTML (W3C Validator)
   - Test light/dark mode
   - Check Lighthouse scores (performance, SEO, accessibility)

7. **Configure Supabase**
   - Set redirect URLs in Supabase dashboard
   - Customize email templates
   - Test email verification flow

---

### Estimated Timeline

**Total Time:** 3-4 hours

| Task | Duration |
|------|----------|
| Project initialization | 30 min |
| Logo extraction & optimization | 30 min |
| Home page implementation | 45 min |
| Privacy policy writing | 45 min |
| Email verification page | 30 min |
| GitHub Pages setup | 30 min |
| Testing & polish | 30 min |

---

### Success Criteria

**Launch Checklist:**

- [ ] Site accessible at `https://subscripto.io`
- [ ] HTTPS enabled (green padlock)
- [ ] All 3 pages functional (home, privacy, verify)
- [ ] Logo displays correctly with green "o"
- [ ] Light/dark mode works (respects system preference)
- [ ] Mobile-responsive (tests on iPhone, Android)
- [ ] Privacy policy comprehensive and readable
- [ ] Email verification flow tested with Supabase
- [ ] App Store buttons hidden (ready to unhide)
- [ ] Lighthouse score 90+ (all metrics)
- [ ] Valid HTML/CSS (no critical errors)
- [ ] Sitemap generated (`/sitemap-index.xml`)
- [ ] Robots.txt present and correct

---

## Appendix

### Package.json Scripts

```json
{
  "name": "subscripto-site",
  "version": "1.0.0",
  "scripts": {
    "dev": "astro dev",
    "build": "astro build",
    "preview": "astro preview",
    "astro": "astro"
  },
  "dependencies": {
    "astro": "^4.0.0",
    "@astrojs/tailwind": "^5.0.0",
    "tailwindcss": "^3.4.0"
  }
}
```

---

### Local Development

```bash
# Install dependencies
npm install

# Start dev server (http://localhost:4321)
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

---

### Resources

**Documentation:**
- Astro: https://docs.astro.build
- Tailwind CSS: https://tailwindcss.com/docs
- GitHub Pages: https://docs.github.com/en/pages
- Supabase Auth: https://supabase.com/docs/guides/auth

**Design System:**
- Material Design 3: https://m3.material.io
- Material Color Tool: https://m2.material.io/design/color

**App Assets:**
- Logo Source: `/SubscriptoApp/composeApp/src/commonMain/composeResources/drawable/`
- Color Scheme: `/SubscriptoApp/composeApp/src/commonMain/kotlin/io/subscripto/subscriptoapp/theme/`

---

### Contact

**Questions/Issues:** Open an issue in the GitHub repository

**Email:** peter@subscripto.io

---

**Document Version:** 1.0
**Last Updated:** December 4, 2024
**Next Review:** After Phase 2 implementation
