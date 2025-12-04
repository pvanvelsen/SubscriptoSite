# Subscripto Website

Official website for Subscripto - Family subscription tracking made simple.

## Overview

This is a static website built with [Astro](https://astro.build) and [Tailwind CSS](https://tailwindcss.com), designed to match the Material 3 branding of the Subscripto mobile app.

## Pages

- `/` - Coming soon landing page
- `/privacy` - Privacy policy
- `/verify` - Email verification redirect (Supabase)

## Tech Stack

- **Framework:** Astro 5.x
- **Styling:** Tailwind CSS 4.x
- **Deployment:** GitHub Pages
- **Domain:** subscripto.io

## Development

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

## Deployment

The site automatically deploys to GitHub Pages via GitHub Actions on push to `main` branch.

### GitHub Pages Setup

1. Repository Settings → Pages
2. Source: GitHub Actions
3. Custom domain: subscripto.io
4. Enforce HTTPS: ✓

### DNS Configuration

Configure at domain registrar:

```
A     @     185.199.108.153
A     @     185.199.109.153
A     @     185.199.110.153
A     @     185.199.111.153
```

## Branding

Colors match the Subscripto mobile app (Material 3):

**Light Mode:**
- Primary: `#1976D2` (Blue 700)
- Secondary: `#4CAF50` (Green 500)
- Background: `#FAFAFA`

**Dark Mode:**
- Primary: `#90CAF9` (Blue 200)
- Secondary: `#66BB6A` (Green 400)
- Background: `#0F0F0F`

Logo: "Subscript**o**" with green "o"

## Supabase Integration

Email verification redirect URL: `https://subscripto.io/verify`

Configure in Supabase Dashboard:
- Authentication → URL Configuration
- Site URL: `https://subscripto.io`
- Redirect URLs: `https://subscripto.io/verify`

## Project Structure

```
├── src/
│   ├── pages/
│   │   ├── index.astro       # Home page
│   │   ├── privacy.astro     # Privacy policy
│   │   └── verify.astro      # Email verification
│   ├── components/
│   │   └── Logo.astro        # Subscripto logo
│   ├── layouts/
│   │   └── BaseLayout.astro  # Base HTML layout
│   ├── styles/
│   │   └── global.css        # Global styles + Tailwind
│   └── content/
│       └── privacy.md        # Privacy policy markdown
├── public/
│   ├── CNAME                 # Custom domain
│   ├── logo.png              # Logo asset
│   └── robots.txt            # SEO
├── doc/
│   └── 01_INITIAL_DEVELOPMENT.md
├── .github/
│   └── workflows/
│       └── deploy.yml        # GitHub Pages deployment
└── astro.config.mjs
```

## Future Enhancements

- `/features` - Feature showcase
- `/pricing` - Pricing tiers
- `/faq` - FAQ page
- `/blog` - Blog

## Contact

- Website: https://subscripto.io
- Email: hello@subscripto.io
- Privacy: privacy@subscripto.io

## License

© 2024 Subscripto. All rights reserved.
