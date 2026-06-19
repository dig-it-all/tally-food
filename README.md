# Putting Tally online — step by step

This guide gets your voice calorie tracker onto the real internet with its own web
address, for free. No coding required. Plan about 15 minutes the first time.

You will do three things:
1. Get an Anthropic API key (the "fuel" for the AI estimates).
2. Upload this folder to a free host called **Vercel**.
3. Next Paste your key into Vercel's settings.

That's it. After that, every time you want changes, I can hand you an updated folder.

---

## What's in this folder

- `index.html` — the app itself (what visitors see).
- `api/estimate.js` — the secure "middleman" that holds your key and talks to Claude.
- `package.json` — a small label file the host reads.
- `README.md` — this guide.

Keep all of these together. Don't rename `api` or `index.html`.

---

## Step 1 — Get your Anthropic API key

1. Go to **https://console.anthropic.com** and sign up (or log in).
2. Add a small amount of prepaid credit under **Billing** — $5 is plenty to start;
   personal use of this app costs roughly pennies a month.
3. Open **API Keys**, click **Create Key**, name it "Tally", and copy the key.
   - It looks like `sk-ant-...`. Copy it somewhere safe for a minute.
   - You'll paste it into Vercel in Step 3. You never put it in any file.

> The key is like a credit card for AI usage — don't share it or post it publicly.
> If it ever leaks, delete it in the console and make a new one.

---

## Step 2 — Upload to Vercel

1. Go to **https://vercel.com** and sign up (the free "Hobby" plan is enough).
   The quickest sign-in is with a Google or GitHub account.
2. On your dashboard, click **Add New… → Project**.
3. Choose the option to **deploy without a Git repository** (look for
   "Deploy" / "Browse" / a drag-and-drop area). Drag this entire folder in,
   or select it.
   - If Vercel only offers GitHub import, see "Alternative" at the bottom.
4. When asked about framework settings, leave them as the defaults
   ("Other" / no build step). Click **Deploy**.
5. After a minute you'll get a live address like `https://tally-xxxx.vercel.app`.
   The page will load, but AI estimates won't work yet — that's Step 3.

---

## Step 3 — Add your key to Vercel

1. In your Vercel project, open **Settings → Environment Variables**.
2. Add one variable:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** paste your `sk-ant-...` key
3. Save. Then go to the **Deployments** tab and **Redeploy** the latest one
   (so it picks up the key).
4. Open your `.vercel.app` address and log a food by voice or text. The
   calories, remaining total, and suggestions should now all work.

Done — that link is yours to use on your phone or share.

---

## Everyday notes

- **Cost control:** in the Anthropic console you can set a monthly spend limit
  and email alerts so there are no surprises.
- **Changing the AI model:** `api/estimate.js` uses `claude-haiku-4-5` (cheapest,
  fast). For slightly richer food suggestions, change that line to
  `claude-sonnet-4-6` and redeploy. Sonnet costs a bit more per use.
- **Custom web address:** Vercel lets you attach your own domain name
  (e.g. `mytally.com`) under Settings → Domains if you buy one.

## Alternative host (Netlify)

Netlify works the same way. Use **Netlify Drop** (drag the folder onto
app.netlify.com/drop), then set the same `ANTHROPIC_API_KEY` under
Site settings → Environment variables. One difference: Netlify expects
serverless files in a folder named `netlify/functions` rather than `api`,
so tell me if you prefer Netlify and I'll relabel the folder for you.

---

If any screen looks different from these steps, take a screenshot or tell me
what you see and I'll walk you through that exact screen.
