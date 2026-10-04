````md
<div align="center">

# 🔍 NxYtVerify v1
### YouTube Screenshot Verification Bot for Discord

**Built by AkiForever**

![Version](https://img.shields.io/badge/Version-1.0.0-black?style=for-the-badge)
![Node](https://img.shields.io/badge/Node.js-18%2B-339933?style=for-the-badge)
![Discord.js](https://img.shields.io/badge/discord.js-v14-5865F2?style=for-the-badge)
![Gemini](https://img.shields.io/badge/Google%20Gemini-AI-4285F4?style=for-the-badge)
![License](https://img.shields.io/badge/License-All%20Rights%20Reserved-red?style=for-the-badge)

</div>

---

## 📌 Overview

**NxYtVerify v1** is a Discord bot that verifies YouTube subscriptions using screenshots.

Users submit a screenshot in the configured verification channel. The bot sends the screenshot to **Google Gemini**, which checks whether the correct YouTube channel is visible and whether the account is actually subscribed.

If the verification passes, the bot automatically gives the configured Discord role.

---

## ✨ Feature Highlights

| Feature | Details |
|---|---|
| 🔍 **Screenshot Verification** | Verifies YouTube subscription screenshots |
| 🤖 **Gemini Verification** | Uses Google Gemini to analyze submitted screenshots |
| 📺 **YouTube Check** | Checks the configured channel name and YouTube handle |
| ✅ **Subscription Check** | Only accepts screenshots showing a subscribed state |
| 🎭 **Auto Role** | Automatically gives the verified Discord role |
| 💬 **DM Results** | Sends the verification result directly to the user |
| 📊 **Logging** | Sends verification results to the configured log channel |
| ⏱️ **Cooldown** | Prevents users from repeatedly submitting screenshots |
| 💾 **Local Data** | Stores verification data locally in JSON |
| 🧹 **Message Cleanup** | Can automatically delete verification messages |
| 🖼️ **Image Validation** | Checks supported image types and maximum image size |

---

## ⚙️ Requirements

- **Node.js** v18 or higher
- **Discord Bot**
- **Discord Bot Token**
- **Google Gemini API Key**
- A Discord server where the bot can manage the verification role

Node.js 20+ is recommended.

---

## 🚀 Installation

### Step 1 — Get the Source Code

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/NxYtVerify-v1.git
cd NxYtVerify-v1
````

Or download the repository as a `.zip` file and extract it.

---

### Step 2 — Install Dependencies

Run:

```bash
npm install
```

If dependencies are not already listed in `package.json`, install them with:

```bash
npm install discord.js @google/genai dotenv
```

---

### Step 3 — Configure Environment Variables

Create a `.env` file in the project folder:

```env
DISCORD_TOKEN=YOUR_DISCORD_BOT_TOKEN
GEMINI_API_KEY=YOUR_GEMINI_API_KEY

VERIFY_CHANNEL_ID=YOUR_VERIFICATION_CHANNEL_ID
VERIFY_ROLE_ID=YOUR_VERIFIED_ROLE_ID

YOUTUBE_CHANNEL_NAME=YOUR_YOUTUBE_CHANNEL_NAME
YOUTUBE_HANDLE=@YOUR_YOUTUBE_HANDLE

LOG_CHANNEL_ID=YOUR_LOG_CHANNEL_ID
```

---

### Step 4 — Start the Bot

```bash
npm start
```

The bot starts using:

```bash
node index.js
```

When the bot starts successfully, the console will show:

```text
======================================
        YT VERIFIER ONLINE
======================================
```

---

## 🔧 Configuration

### Environment Variables

| Variable               | Description                                |
| ---------------------- | ------------------------------------------ |
| `DISCORD_TOKEN`        | Discord bot token                          |
| `GEMINI_API_KEY`       | Google Gemini API key                      |
| `VERIFY_CHANNEL_ID`    | Channel where users submit screenshots     |
| `VERIFY_ROLE_ID`       | Role given after successful verification   |
| `YOUTUBE_CHANNEL_NAME` | YouTube channel users need to subscribe to |
| `YOUTUBE_HANDLE`       | YouTube handle of the required channel     |
| `LOG_CHANNEL_ID`       | Channel where verification logs are sent   |

---

### Bot Configuration

Additional verification settings are stored in:

```text
config.js
```

The configuration includes:

```text
maxImageSize
cooldownMs
allowedMimeTypes
geminiModel
deleteScreenshotAfterVerification
```

These settings control:

* Maximum screenshot size
* Verification cooldown
* Allowed image formats
* Gemini model
* Automatic screenshot/message deletion

---

## 🔍 How Verification Works

When a user sends a screenshot in the verification channel, NxYtVerify checks it step by step.

### 1. Image Check

The bot checks whether the message contains a supported image.

### 2. Image Size Check

The image is checked against the configured maximum image size.

### 3. Verification Status

The bot checks whether the user has already been verified.

### 4. Cooldown

The bot checks whether the user has recently attempted verification.

### 5. Gemini Analysis

The screenshot is sent to Google Gemini.

Gemini checks:

* Whether the screenshot is from YouTube
* Whether the correct channel is visible
* Whether the channel matches the configured name
* Whether the channel matches the configured handle
* Whether the subscription state is visible
* Whether the state shows `Subscribed`

### 6. Verification Result

The bot receives a JSON result containing:

```json
{
  "valid": true,
  "confidence": 95,
  "reason": "The screenshot clearly shows the correct channel with the Subscribed state."
}
```

### 7. Role Assignment

If the verification is valid, the configured verified role is given to the user.

### 8. DM Result

The user receives the verification result through Discord DM.

### 9. Logging

The result can also be sent to the configured log channel.

### 10. Cleanup

If enabled, the original verification message can be deleted automatically.

---

## ❌ Verification Rules

The bot only approves a screenshot when the subscription can be clearly confirmed.

A screenshot showing:

```text
Subscribe
```

is rejected.

The bot can also reject screenshots that are:

* Unrelated to YouTube
* Showing the wrong channel
* Too blurry to verify
* Missing the channel identity
* Missing a clear subscription state
* Showing an unclear subscription status
* Invalid or manipulated-looking

Simply showing a YouTube video or channel is **not enough**.

The subscription state must be visible.

---

## 📊 Logging

If `LOG_CHANNEL_ID` is configured, verification results are sent to that channel.

Logs can contain:

* User
* Verification result
* Gemini confidence
* Verification reason
* DM result

---

## ⏱️ Cooldown

NxYtVerify includes a cooldown system to prevent repeated verification attempts.

Attempt timestamps are stored locally.

The verification data is saved in:

```text
data/verifications.json
```

---

## 💾 Data Storage

NxYtVerify uses a local JSON file instead of an external database.

The file is:

```text
data/verifications.json
```

The default structure is:

```json
{
  "verified": {},
  "attempts": {}
}
```

The bot automatically creates the `data` folder and database file if they do not exist.

If you move the bot to another host and want to keep the existing verification records, move the `data` folder with the bot.

---

## 🧹 Screenshot Cleanup

NxYtVerify can automatically delete verification messages after processing.

This is controlled by:

```text
deleteScreenshotAfterVerification
```

inside:

```text
config.js
```

---

## 🔐 Discord Permissions

The bot needs access to the configured verification channel.

It also needs permission to manage the configured verification role.

Make sure the bot's highest role is **above** the verification role.

Otherwise Discord will prevent the bot from assigning the role.

If automatic cleanup is enabled, the bot also needs permission to delete messages.

---

## 🔑 Security

Never upload your real `.env` file to GitHub.

Your `.env` contains private credentials such as:

```text
DISCORD_TOKEN
GEMINI_API_KEY
```

Add this to `.gitignore`:

```gitignore
node_modules/
.env
data/verifications.json
*.log
```

If your Discord bot token is exposed, reset it immediately.

If your Gemini API key is exposed, revoke or replace it.

---

## 📁 Project Structure

```text
NxYtVerify-v1/
│
├── index.js                  # Main bot file
├── config.js                 # Verification configuration
├── package.json              # Node.js project configuration
├── README.md                 # Project documentation
├── LICENSE                   # Project license
│
└── data/
    └── verifications.json    # Verification data
```

---

## 🛠️ Technologies

* **Node.js**
* **Discord.js**
* **Google Gemini**
* **dotenv**
* **JSON storage**

---

## 🚀 Running the Bot

### Production

```bash
npm start
```

### Direct Start

```bash
node index.js
```

---

## 📝 Notes

NxYtVerify is designed for screenshot-based YouTube subscription verification.

The verification result depends on what can actually be determined from the submitted screenshot.

Gemini does not automatically guarantee that a screenshot is genuine. Server owners should configure and use the verification system according to their own requirements.

---

## 👤 Developer

**AkiForever**

### Project

**NxYtVerify v1**

---

## 📜 License & Legal

```text
Copyright © 2026 AkiForever. All Rights Reserved.

NxYtVerify v1 and its original source code, configuration,
documentation and original assets are the property of AkiForever.

You may download, view, study, modify and run the project for
personal use.

You may create private modifications and private forks.

Public forks are allowed for non-commercial use only, provided
that the original author credit and license remain included.

You may NOT:

- Sell the original project.
- Sell modified versions of the project.
- Re-upload the project and claim it as your own.
- Remove the original author attribution.
- Remove or replace this license.
- Redistribute the project commercially.
- Package the project as a paid product.
- Use the NxYtVerify name to impersonate the original project.
- Claim the original NxYtVerify source code as your own.

Commercial use requires written permission from AkiForever.

Third-party packages and services used by NxYtVerify are subject
to their own licenses and terms.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.

Copyright © 2026 AkiForever.
All Rights Reserved.
```

---

## ⚠️ Disclaimer

NxYtVerify is an independent project.

It is not affiliated with:

* Discord
* YouTube
* Google
* Google Gemini

You are responsible for your own bot, API keys, Discord server configuration, and use of this software.

---

<div align="center">

**NxYtVerify v1**

**© 2026 AkiForever — All Rights Reserved**

Made by **AkiForever**

</div>
```
