# What Should We Be Talking About?

A live website that checks the DOW Jones and applies AG Pam Bondi's own standard:

- **DOW ≥ 50,000** → "We should be talking about THE DOW"
- **DOW < 50,000** → "We should be talking about JEFFREY EPSTEIN"

Updates every 30 seconds during market hours.

## Deploy to Netlify (Step by Step)

### 1. Push to GitHub

1. Go to [github.com/new](https://github.com/new) and create a new repository (e.g. `bondi-dow-tracker`)
2. Upload all the files from this folder maintaining this structure:
   ```
   bondi-dow-tracker/
   ├── netlify.toml
   ├── package.json
   ├── public/
   │   └── index.html
   └── netlify/
       └── functions/
           └── dow.js
   ```

### 2. Connect to Netlify

1. Go to [app.netlify.com](https://app.netlify.com)
2. Click **"Add new site"** → **"Import an existing project"**
3. Choose **GitHub** and select your repository
4. Build settings should auto-detect from `netlify.toml`:
   - Publish directory: `public`
   - Functions directory: `netlify/functions`
5. Click **Deploy**

### 3. Set your Finnhub API key as an environment variable

1. In Netlify, go to **Site settings** → **Environment variables**
2. Add a new variable:
   - Key: `FINNHUB_API_KEY`
   - Value: `your-finnhub-api-key`
3. Trigger a redeploy: **Deploys** → **Trigger deploy** → **Deploy site**

### 4. (Optional) Custom domain

In Netlify: **Domain management** → **Add custom domain**

## How It Works

- A Netlify serverless function (`/api/dow`) fetches the DIA ETF price from Finnhub
- DIA tracks the DOW at ~1/100th the value, so we multiply to estimate the DOW
- The frontend calls this function every 30 seconds
- The page dynamically switches between Epstein mode (red) and DOW mode (green)
