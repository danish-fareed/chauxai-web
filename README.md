# ChauxAI Web — Vercel Frontend

A standalone web frontend for **ChauxAI** that connects to your **local Python agent** to download, split, and process videos into viral short-form clips.

## How it Works

```
[Vercel Web App] ──── HTTP/SSE ───▶ [Your Local Agent: python app.py]
  (deployed online)   (you configure    (processes video with ffmpeg,
  open in browser)    the URL once)      yt-dlp, OpenAI — all local)
```

The web app is **purely static** — it runs in your browser and talks to your local machine. No video data is ever uploaded to Vercel.

---

## Setup (2 steps)

### Step 1 — Run your local agent

In your `automation_scripts` folder:

```bash
# Activate virtual environment
.\venv\Scripts\activate

# Install dependencies (first time only)
pip install -r requirements.txt

# Start the agent
python app.py
```

The agent starts on `http://localhost:5000` by default.

> **Note:** Keep this terminal running whenever you use the web app.

### Step 2 — Open the web app and connect

1. Open your Vercel deployment URL (or `index.html` locally in a browser)
2. A **"Connect Your Agent"** setup screen appears on first load
3. Enter your agent URL:
   - **Same PC:** `http://localhost:5000`
   - **Different device on same WiFi:** `http://192.168.1.XXX:5000` (find your PC's IP with `ipconfig`)
4. Click **Connect →**

The URL is saved in your browser's `localStorage` and remembered for future visits.

---

## Deploying to Vercel

### Option A — Vercel CLI

```bash
npm i -g vercel
vercel --cwd d:\chauxai-web
```

### Option B — Vercel Dashboard

1. Push this folder to a GitHub repo
2. Go to [vercel.com](https://vercel.com) → **New Project**
3. Import the repo — Vercel auto-detects it as a static site
4. Deploy — done!

---

## Connecting from a different device (phone, tablet, etc.)

If you open the Vercel URL on your phone, you need to make your local agent reachable:

1. Find your PC's local IP: run `ipconfig` → look for **IPv4 Address** (e.g. `192.168.1.42`)
2. Make sure your phone and PC are on **the same WiFi network**
3. Enter `http://192.168.1.42:5000` as the agent URL in the setup screen

> **Tip:** Windows Firewall may block port 5000. Allow it with:
> ```
> netsh advfirewall firewall add rule name="ChauxAI Agent" dir=in action=allow protocol=TCP localport=5000
> ```

---

## Changing the agent URL later

Click **Agent Connection** in the sidebar at any time to update the URL.

---

## Project Structure

```
chauxai-web/
├── index.html      ← Complete SPA (pure HTML/CSS/JS, no build step)
├── vercel.json     ← Vercel routing config
└── README.md       ← This file
```
