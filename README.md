# PowderTracks Website

Official website for PowderTracks - the free ski tracking app.

🌐 **Live Site**: https://powdertracks.com

## 🚀 Quick Start

### Local Development

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/powdertracks-website.git
cd powdertracks-website

# Open in browser
open index.html
# or just double-click index.html
```

That's it! No build process, no dependencies, just pure HTML/CSS/JS.

## 📦 Deployment

This site automatically deploys to Cloudflare Pages via GitHub Actions on every push to `main`.

### First-Time Setup

1. **Create Cloudflare Pages Project**
   - Login to Cloudflare Dashboard
   - Go to Pages → Create Project
   - Connect to your GitHub repo
   - Project name: `powdertracks`
   - Build settings: None needed (static site)

2. **Add GitHub Secrets**
   
   In your GitHub repo: Settings → Secrets and variables → Actions
   
   Add these secrets:
   ```
   CLOUDFLARE_API_TOKEN=your_api_token_here
   CLOUDFLARE_ACCOUNT_ID=your_account_id_here
   ```
   
   **Get API Token:**
   - Cloudflare Dashboard → Profile → API Tokens
   - Create Token → Use "Edit Cloudflare Workers" template
   - Or create custom token with `Account.Cloudflare Pages: Edit` permission
   
   **Get Account ID:**
   - Cloudflare Dashboard → Any domain → Right sidebar shows "Account ID"

3. **Push to GitHub**
   ```bash
   git add .
   git commit -m "Initial commit"
   git push origin main
   ```
   
   GitHub Actions will automatically deploy to Cloudflare Pages!

### Manual Deployment

You can also deploy manually using Wrangler CLI:

```bash
# Install Wrangler
npm install -g wrangler

# Login to Cloudflare
wrangler login

# Deploy
wrangler pages deploy . --project-name=powdertracks
```

## 📁 Project Structure

```
powdertracks-website/
├── index.html              # Main landing page
├── style.css               # Styles with charcoal/orange theme
├── script.js               # JavaScript for interactivity
├── privacy.html            # Privacy policy
├── images/
│   └── logo.png           # PowderTracks logo
├── .github/
│   └── workflows/
│       └── deploy.yml     # GitHub Actions workflow
└── README.md              # This file
```

## 🎨 Color Scheme

- **Charcoal**: #2C2C2C (main dark color)
- **Orange**: #FF6B35 (accent color)
- **White**: #FFFFFF
- **Light Gray**: #F5F5F5

## ✨ Features

- ❄️ Falling snow animation
- 📱 Fully responsive design
- 🎨 Charcoal and orange branding
- 🚀 Auto-deploy via GitHub Actions
- ⚡ Fast loading (no dependencies)

## 🛠️ Making Changes

1. Edit files locally
2. Test by opening index.html in browser
3. Commit and push to GitHub
4. GitHub Actions automatically deploys to Cloudflare Pages
5. Changes live in ~1 minute!

## 📝 TODO

- [ ] Add actual App Store and Google Play links when apps are ready
- [ ] Create privacy policy content
- [ ] Add app screenshots/demo video
- [ ] Set up analytics (optional)
- [ ] Add blog section for updates (optional)

## 🤝 Contributing

This is a personal project, but suggestions are welcome! Open an issue or submit a PR.

## 📄 License

© 2026 PowderTracks. All rights reserved.

---

Built with ❤️ in Colorado 🏔️
