# AI Chat (Gemini) — Web App / PWA

🇺🇸 English · 🇧🇷 [Português](README.pt-BR.md)

A progressive web app (PWA) for chatting with AI. It runs entirely in the browser, talks directly to the Google Gemini API, and keeps long-term memory on your own device (IndexedDB). It supports multiple conversations, voice input and spoken replies, images, and documents.

---

## 🚀 Features

**Chat**
- Multiple conversations: create, rename and delete them from the ☰ menu.
- Three Gemini models to choose from (3.5 Flash Lite, 3.6 Flash, 3.8 Flash).
- Temperature slider and adjustable context (how many previous messages of the open conversation are sent).
- Editable system prompt ("Personality"), with a "Restore default" button.
- AI reply language: same as your message (default), English or Portuguese.

**Long-term memory (shared by all conversations)**
- Messages from every conversation feed one memory queue.
- When 20 messages are waiting, the AI condenses the 15 oldest into up to 5 *Permanent* memories and up to 5 *Profile* facts about you.
- When Permanent or Profile reach 20 items, they are condensed again into 5.
- Every conversation sees the same Profile and Permanent memories. Chat history stays per conversation.
- A counter shows how many messages are waiting to be summarized (for example `7/20`).
- The ☰ menu has a collapsible **Not yet summarized** panel that lists those waiting messages from all conversations. Delete the ones you don't want remembered, so junk never reaches your Permanent or Profile memories. Deleting there only keeps a message out of memory; it stays in the chat.
- **Memories** (in ⚙) lists the Permanent and Profile memories and shows the same counter.
- In all three lists (not yet summarized, Permanent, Profile) you can delete items one by one, select several, or delete all.
- Deleting a conversation does not delete memories already extracted from it.

**Voice**
- 🎤 Speech recognition: tap, speak, and the text is sent when you stop (this can be turned off).
- 🔊 Spoken replies: read automatically or per message, with **speed control (0.5×–2×)** and a choice of voice.
- Hands-free mode: listen → reply → speak → listen again.
- Voice language is set separately from the interface language (12 options).

**Images and files**
- 📎 Attach images (camera or gallery on a phone; paste or drag-and-drop on a PC). Images are compressed on the device before sending.
- PDF: sent directly to Gemini (up to ~14 MB).
- Word (`.docx`) and OpenDocument (`.odt`): text is extracted in the browser.
- Text files: `.txt`, `.md`, `.csv`, `.json`, `.html`, source code and similar (first 300,000 characters).
- Full attachment contents are sent only for the last 2 messages that have attachments; older ones appear to the AI as a file name.

**Interface and PWA**
- English (default) and Portuguese (BR) interface.
- Install button for phone or PC. A service worker caches the app shell (chatting still needs internet).
- Export / Import of all chats and memories (backups from older versions can be imported too).

---

## 📂 Project files

| File | Purpose |
|---|---|
| `index.html` | The whole app: interface, styles, chat logic, IndexedDB |
| `manifest.json` | PWA manifest: name, colors, icons |
| `sw.js` | Service worker: caching and offline fallback |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | App icons (needed for the install option to appear) |

---

## 🧰 Libraries and requirements

**The app has no dependencies:** no npm packages, no build step, no backend, no CDN. It is plain HTML, CSS and JavaScript that uses built-in browser features.

What you do need:

- **A modern Chromium-based browser** (Google Chrome recommended; Microsoft Edge also works).
  - Speech recognition uses the browser's Web Speech API. It is available in Chrome and Edge, but not in Firefox. On iPhone/iOS it is unreliable.
  - Reading `.docx`/`.odt` needs a browser from the last few years (Chrome 103 or newer).
- **HTTPS or `localhost`.** Browsers only allow the microphone, the service worker and installation on a secure origin. Opening `index.html` by double-clicking (`file://`) or from a local network address such as `http://192.168.x.x` will **not** support these.
- **Internet connection.** Chat uses the Gemini API, and Chrome's speech recognition is processed on Google's servers.
- **A Gemini API key** from [Google AI Studio](https://aistudio.google.com/apikey).
- **Only for Option 2 below:** a way to serve the files locally. Python 3 (usually already installed) or Node.js works. Any static file server will do.

---

## 🔒 Privacy

- Chats, memories and attachments are stored only in your browser (IndexedDB). Your API key is stored in the browser's localStorage.
- Messages, attachments and memories are sent to Google's Gemini API to generate replies. Voice input is sent to Google's speech service by Chrome.
- Anyone with access to your browser profile can read the saved API key. Use **Export** for backups and keep them private, because they contain your conversations and attachments.

---

## 🛠️ How to use

### 🔑 First steps (both options)

1. Create an API key in [Google AI Studio](https://aistudio.google.com/apikey).
2. Open the app, tap ⚙, paste the key into **Paste your Gemini API key here**, and tap **Save key**.
3. Choose the model, temperature, voice and personality, and start chatting.

### Option 1 — Use the Vercel website (easiest)

1. Open **https://app-viva-ia.vercel.app** in Google Chrome on your PC or phone.
2. Phone: tap **Install app** (or Chrome menu ⋮ → *Install app* / *Add to Home screen*). PC: click the install icon in the address bar.
3. Open the app, add your API key (see *First steps*), and start chatting.

Vercel serves the app over HTTPS, so the microphone, installation and offline cache work with no setup.

### Option 2 — Clone or download the files and install on your PC

1. Get the files: clone the repository, or click **Code → Download ZIP** on GitHub and extract it.

   ```bash
   git clone https://github.com/YOUR-USER/YOUR-REPO.git
   cd YOUR-REPO
   ```

2. Make sure `index.html`, `manifest.json`, `sw.js` and the three `icon-*.png` files are in the same folder.
3. Start a local server in that folder (pick one):

   ```bash
   python3 -m http.server 8000      # Linux / macOS (Windows: python -m http.server 8000)
   npx serve -l 8000                # alternative, needs Node.js
   ```

4. Open **http://localhost:8000** in Chrome, then click the install icon in the address bar (or ⋮ → *Install AI Chat*).
5. Add your API key (see *First steps*).

Notes for Option 2:
- Always use the **same address and port**. Your chats and settings are tied to it (`localhost:8000` and `localhost:8001` are different apps with separate data).
- After installing, the app also opens while the server is stopped, thanks to the cache. To get updated files, start the server again and reload.
- After replacing the files with a new version, open the app once with the server running and then fully close and reopen it, so the new service worker takes over.

---

## ❓ Troubleshooting

- **Microphone does nothing:** check that you are on HTTPS or `localhost`, that microphone permission is allowed for the site, and that you are using Chrome or Edge.
- **Speech is transcribed in the wrong language:** set ⚙ → *Voice language* to the language you are speaking. It does not detect the language automatically.
- **A voice or language is missing for spoken replies:** voices come from your device. On Android, install the language's voice data in the system text-to-speech settings.
- **The page looks translated:** the app asks Chrome not to translate it. If Chrome remembered a translation for the site, use ⋮ → *Show original*.
- **The AI answers in the wrong language:** check ⚙ → *AI reply language* and the *Personality* text (a personality written in another language pulls replies toward it; use *Restore default* to reset it). Test in a new chat, because earlier replies in the same chat also influence the language.
- **A PDF is rejected:** the limit is about 14 MB. Split the file or compress it.
- **Not supported:** old `.doc`, `.xlsx`, `.pptx`, HEIC photos, and the live streaming of replies (a reply appears when complete).
