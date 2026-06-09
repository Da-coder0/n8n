# Batch Image Generator — Setup Guide

## What this workflow does

1. You open a form, upload a CSV of prompts + your character reference image
2. Every prompt is sent to **Kie AI Nano Banana 2** with your character as the reference
3. All images are collected, zipped, and sent to your email
4. The ZIP is also available to download directly from the form page

---

## Step 1 — Import the workflow

1. Open your n8n instance
2. Go to **Workflows → Import**
3. Upload `batch-image-generator.workflow.json`

---

## Step 2 — Add your Kie AI API key

1. Sign up / log in at [kie.ai](https://kie.ai) and get your API key
2. In n8n, go to the **Batch Generate** Code node
3. At the top of the code, replace `'PASTE_YOUR_KIE_API_KEY_HERE'` with your key

   OR (recommended) add it as an environment variable in your n8n config:
   ```
   KIE_API_KEY=your_key_here
   ```

---

## Step 3 — Connect your email

The workflow uses **Gmail** by default. To connect it:

1. Click the **Send Email** node
2. Click **Create new credential → Gmail OAuth2**
3. Follow the Google OAuth flow

**If you prefer SMTP** (e.g. Outlook, custom domain):
- Delete the Gmail node
- Add an **Email Send (SMTP)** node instead
- Connect your SMTP credentials in n8n settings

---

## Step 4 — Activate the workflow

1. Click **Activate** (top right toggle in n8n)
2. Click the **Form** node to get your form URL
3. Share that URL with yourself — bookmark it

---

## CSV format

Your CSV should have one prompt per row. A header row is optional and auto-detected.

**Example:**
```
prompt
A heroic warrior standing on a mountain cliff at sunset
The character running through a neon-lit cyberpunk city at night
A close-up portrait with dramatic studio lighting
```

The first column is always used. You can have other columns — they are ignored.

---

## Costs (Kie AI Nano Banana 2)

| Images | Estimated Cost |
|--------|---------------|
| 100    | ~$2–4         |
| 500    | ~$10–20       |
| 1,000  | ~$20–40       |

Buy credits at [kie.ai/pricing](https://kie.ai/pricing) — pay as you go, no subscription.

---

## How long does it take?

- Task submission: ~0.35s per prompt (35s for 100 prompts)
- Generation: all tasks run in parallel on Kie AI, typically **30–90 seconds total**
- Image download + ZIP: ~1–2 minutes for 100 images
- **Total: usually under 5 minutes for 100 images**

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| "No URL returned" after upload | Check your API key has credits and is correct |
| Images missing from ZIP | Some prompts may have failed — check execution logs in n8n |
| Email not sending | Re-connect your Gmail credential or switch to SMTP |
| Form not accessible | Make sure the workflow is **Activated** in n8n |
