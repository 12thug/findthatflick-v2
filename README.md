# 🍿 FindthatFlick

> A sleek, single-file web app to search movies, games, books & software across multiple sites — with an AI movie assistant powered by Groq (free).

![FindthatFlick Preview](https://i.imgur.com/placeholder.png)

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔍 **Multi-site Search** | Searches movies, games, books & software across 8+ sites simultaneously |
| 🤖 **Chris AI Assistant** | Powered by Groq (free) — get personalized movie recommendations |
| 🎬 **Video Background** | Cinematic YouTube video background with glassmorphism cards |
| 🏷️ **Taste Tags** | Select genre preferences (Action, Drama, Sci-Fi…) that are silently added to every AI prompt |
| 🕓 **Recent Searches** | Last 5 searches saved locally — click to re-use instantly |
| 📱 **Responsive** | Works on desktop and mobile |

---

## 🚀 Getting Started

### 1. Download
Just download `findthatflick.html` — it's a **single self-contained file**. No install, no dependencies, no server needed.

### 2. Open
Double-click `findthatflick.html` to open it in your browser.  
Works in Chrome, Edge, Firefox, Safari.

> ⚠️ **Pop-ups required** — The search function opens multiple tabs. Allow pop-ups for the file when prompted.

### 3. Get a Free AI Key (optional but recommended)
Chris AI uses **Groq** — 100% free, no credit card needed.

1. Go to **[console.groq.com](https://console.groq.com)**
2. Sign up (Google login works)
3. Click **API Keys** → **Create API Key**
4. Copy the key (starts with `gsk_...`)
5. Click **"🔑 Connect API"** in the app and paste it

Your key is stored **only in your browser session** (sessionStorage) — never sent anywhere except Groq's API directly.

---

## 🔍 How Search Works

The search feature uses **Google Dork queries** — it opens multiple tabs, each searching a different site for your query.

### Categories & Sites

| Category | Sites Searched |
|---|---|
| **Movies** | psa.wf, pahe.ink, olamovies.blog, vegamovies, uhdmovies, katmoviehd, hdhub4u, 4khdhub |
| **Games** | fitgirl-repacks.site, koyso.to |
| **Books** | libgen.is, z-lib.org, b-ok.cc, epdf.pub |
| **Software** | filehippo.com, softpedia.com, techspot.com |

### How to Search
1. Type the media name in **"Enter a Name"**
2. Select a category from the dropdown
3. Click **"Search All Sites"**
4. Multiple tabs open — each searches a different site

---

## 🤖 Chris AI Assistant

Chris is an AI movie & entertainment guide powered by **Groq's `llama-3.3-70b-versatile`** model.

### How to Use
1. Click **"🔑 Connect API"** and paste your Groq key
2. Optionally tap **Taste Tags** (Action, Drama, Sci-Fi…) to pre-set your preferences
3. Type anything in the chat — "What should I watch tonight?" or "Something like Interstellar"
4. Chris remembers the full conversation for multi-turn chat

### Taste Tags
Tags you select are **silently prepended** to every prompt:
```
[My taste preferences: Action, Sci-Fi]
What should I watch tonight?
```
This means Chris always factors in your genre preferences without you having to repeat them.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | Pure HTML + CSS + Vanilla JavaScript (zero dependencies) |
| **Fonts** | Syne (headers) + DM Sans (body) via Google Fonts |
| **Background** | YouTube iframe embed (muted autoplay) |
| **Glassmorphism** | CSS `backdrop-filter: blur()` on semi-transparent cards |
| **AI** | Groq API — `llama-3.3-70b-versatile` model |
| **Storage** | `localStorage` for recent searches + popup preference; `sessionStorage` for API key |

---

## 📁 File Structure

```
findthatflick.html          ← Entire app in one file
README.md                   ← This documentation
```

Everything is self-contained in a single `.html` file:
- All CSS is in `<style>` tags
- All JavaScript is in `<script>` tags  
- The popcorn favicon is embedded as a base64 data URI
- No external CSS frameworks, no npm, no build step

---

## ⚙️ Configuration

All configurable values are at the top of the `<script>` section:

```javascript
// AI model — change to any Groq-supported model
model: 'llama-3.3-70b-versatile'

// Max AI response length (tokens)
max_tokens: 320

// AI creativity (0.0 = deterministic, 1.0 = very creative)
temperature: 0.9

// Number of recent searches to remember
const MAX_RECENT = 5;
```

### Changing the Background Video
Find this line in the HTML and replace `3aAvQxtvKiA` with any YouTube video ID:
```html
src="https://www.youtube.com/embed/3aAvQxtvKiA?autoplay=1&mute=1&loop=1&playlist=3aAvQxtvKiA&controls=0&rel=0&start=8"
```
> The video ID appears **twice** in the URL (once in the path, once in `&playlist=`). Change both.

### Adding Search Sites
In the `searchBtn` click handler, add URLs to the relevant array:
```javascript
if (cat === 'movies') {
    urls = [
        // add your site here:
        `https://yoursite.com/search?q=${q}`,
        ...
    ];
}
```

### Changing the AI System Prompt
Find `SYSTEM_PROMPT` in the script and edit it:
```javascript
const SYSTEM_PROMPT = `You are Chris, a friendly movie recommendation assistant...`;
```

---

## 🐛 Known Issues & Fixes

| Issue | Cause | Fix |
|---|---|---|
| YouTube Error 153 | Extra params like `enablejsapi=1` without a valid `https://` origin | Use minimal embed params only |
| Search tabs blocked | Browser blocking pop-ups | Allow pop-ups for the file in browser settings |
| AI quota exceeded | Groq/Gemini/OpenAI free tier limits | Get a new API key from console.groq.com (free) |
| Backdrop blur not visible | Card background opacity too high | Keep `--card-bg` opacity below 0.55 |

---

## 🔑 API Key Notes

- **Groq** (current): Free, no billing needed. Get at [console.groq.com](https://console.groq.com)
- **Gemini**: Free tier (1500 req/day) but can hit quota. Get at [aistudio.google.com](https://aistudio.google.com)
- **OpenAI**: Requires billing. Get at [platform.openai.com](https://platform.openai.com)

To switch APIs, update the `callDeepSeek()` function in the script with the relevant endpoint, auth header format, and response parsing.

---

## 📜 Changelog

| Version | Changes |
|---|---|
| v1.0 | Initial single-card search UI with YouTube background |
| v1.1 | Fixed JS bug — missing comma in movies URL array caused entire search to break |
| v2.0 | Redesigned to dual-card layout; added Chris AI chat with glassmorphism |
| v2.1 | Added taste tags, Connect API button (on-demand modal) |
| v2.2 | Fixed card overflow; brand text clamp; white accent colours |
| v2.3 | Video fix (Error 153); DeepSeek → OpenAI → Gemini → Groq API migrations |
| v2.4 | Reordered search fields; added Recent Searches; popcorn favicon; this README |

---

## 👤 Credits

**Created by vsx**

---

## 📄 License

Personal/private use. Not for redistribution.
