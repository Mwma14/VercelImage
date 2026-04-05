# Bot Image Proxy (Vercel)

This is a minimal Vercel project that acts as an **HTTPS proxy** for the Telegram bot image server running at `http://2.56.246.128:30200`.

It allows the website (hosted on ezsite.ai or any HTTPS platform) to load images from the bot server without Mixed Content errors.

## How It Works

All requests to `https://your-proxy.vercel.app/...` are forwarded to `http://2.56.246.128:30200/...`.

For example:
```
https://your-proxy.vercel.app/5097?hash=AgADeg
        ↓ proxied to ↓
http://2.56.246.128:30200/5097?hash=AgADeg
```

## Deploy to Vercel

### Option 1: Vercel CLI
```bash
npm install -g vercel
cd vercel-proxy
vercel --prod
```

### Option 2: Vercel Dashboard (No CLI needed)
1. Go to [vercel.com](https://vercel.com) and sign in
2. Click **Add New Project**
3. Upload this folder (or push to GitHub first)
4. Click **Deploy** — no build settings needed

### After Deployment
You will get a URL like: `https://bot-image-proxy.vercel.app`

**Update the website's `proxyImageUrl` function** in:
- `src/components/VideoCard.tsx`
- `src/pages/VideoDetail.tsx`

Replace `YOUR_VERCEL_PROXY_URL` with your actual Vercel URL:
```js
return url.replace('http://2.56.246.128:30200', 'https://YOUR_VERCEL_PROXY_URL');
```

## Update Bot URL (Optional)
Once the proxy is deployed, you can also update the bot's `URL` in `.env`:
```
URL=https://your-proxy.vercel.app/
```
This makes the bot generate HTTPS links directly.
