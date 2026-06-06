# 🎬 YouTube Shorts → Instagram Reels Automation

> Automatically cross-post your YouTube Shorts to Instagram Reels using Make.com — zero manual effort after setup.

![Make.com](https://img.shields.io/badge/Make.com-6C2BD9?style=for-the-badge&logo=make&logoColor=white)
![YouTube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)
![Instagram](https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white)

---

## 📌 What This Does

Every time you upload a YouTube Short, this automation:

1. **Detects** the new video on your YouTube channel
2. **Filters** it (only Shorts under 61 seconds pass through)
3. **Fetches** the direct MP4 download URL via RapidAPI
4. **Posts** it to your Instagram account as a Reel — with the same title as the caption

All of this happens automatically every 4 hours. No manual work needed.

---

## 🔁 Flow Overview

```
YouTube (Watch Channel) 
    ↓
[Filter: duration < 61s]
    ↓
HTTP Request (YT-API on RapidAPI → get MP4 URL)
    ↓
Instagram for Business (Create Reel Post)
```

---

## 🚀 Quick Start

### Step 1 — Import the Scenario into Make.com

Click the link below to open the shared scenario directly in Make.com:

👉 **[Import Scenario](https://eu1.make.com/public/shared-scenario/412Di24w1xz/integration-you-tube)**

<img width="1875" height="922" alt="image" src="https://github.com/user-attachments/assets/d55fc23a-53c2-41a3-9795-489e7789011a" />


### Step 2 — Connect Your Accounts

You'll need to connect three things inside Make.com:

| Connection | What it's for |
|------------|---------------|
| YouTube (Google OAuth) | Watch your channel for new videos |
| Instagram for Business (Facebook login) | Post Reels to your Instagram page |
| RapidAPI Key | Fetch the direct MP4 URL of the Short |

### Step 3 — Get a RapidAPI Key

1. Go to [rapidapi.com](https://rapidapi.com) and sign up (free)
2. Search for **"YT-API"** by ytjar
3. Subscribe to the **free plan**
4. Copy your API key from the dashboard

### Step 4 — Configure the HTTP Module

Inside the imported scenario, open the **HTTP module** and set the headers:

| Header Name | Header Value |
|-------------|--------------|
| `x-rapidapi-host` | `yt-api.p.rapidapi.com` |
| `x-rapidapi-key` | `YOUR_RAPIDAPI_KEY_HERE` |

### Step 5 — Set Your YouTube Channel ID

In the YouTube module, replace the Channel ID with your own. You can find it by:
- Going to your YouTube channel
- Clicking "More" → "About" → "Share channel" → "Copy channel ID"

### Step 6 — Set Your Instagram Page

In the Instagram module, select your Instagram Business page from the dropdown.

### Step 7 — Turn It On

Hit the toggle at the bottom of Make.com to activate the scenario. It will run every 4 hours automatically.

---

## ⚙️ Module Details

### 1. YouTube — Watch Videos in a Channel
- Polls your channel every 24 hours
- Picks up the latest video (limit: 1)

### 2. Filter — Shorts Only
- Condition: `duration < 61` (number)
- Ensures only Shorts (≤60 seconds) pass through
- Long videos are automatically skipped

### 3. HTTP — Make a Request
- **URL:** `https://yt-api.p.rapidapi.com/dl?id={{videoId}}`
- **Method:** GET
- **Parse Response:** Yes
- Returns the direct MP4 URL of the Short

### 4. Instagram for Business — Create a Reel Post
- **Video URL:** `{{3.data.formats[].url}}` (from HTTP response)
- **Caption:** `{{1.title}}` (same as YouTube title)
- **Share to Feed:** Yes

---

## 🛠️ Requirements

- A [Make.com](https://make.com) account (free tier works)
- A YouTube channel with a Google account
- An Instagram **Business** or **Creator** account (personal accounts won't work)
- A Facebook Page connected to your Instagram account
- A [RapidAPI](https://rapidapi.com) account (free tier — 300 requests/month)

---

## ❓ Troubleshooting

**YouTube module runs but nothing passes to HTTP**
→ The latest video on your channel is longer than 61 seconds. The filter is working correctly — it will pass through when you upload a Short.

**HTTP module returns 403**
→ You passed a full YouTube URL instead of just the video ID. Make sure the YouTube module's `videoId` field is mapped correctly (not the full URL).

**Instagram module fails**
→ Make sure your Instagram account is a Business/Creator account and is connected to a Facebook Page.

**Nothing runs at all**
→ Check that the scenario is turned ON (toggle at the bottom of Make.com). Also check "Where to start" on the YouTube module is set to "From now on" or "All".

---

## 📦 Tech Stack

- **Make.com** — automation platform
- **YouTube Data API** (via Make.com native module)
- **YT-API on RapidAPI** — fetches direct MP4 download URLs
- **Instagram Graph API** (via Make.com Instagram for Business module)

---

## 📄 License

MIT License — free to use, modify, and share.

---

## 🌟 Star This Repo

If this saved you time, drop a ⭐ on the repo — it helps others find it!
