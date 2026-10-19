# Copilot (iPhone web app)

Listens to the interviewer's question and shows a text answer built from your resume, plus a web-searched version. Nothing else.

## How it stays fast
1. Hands-free: it listens continuously and detects when the speaker pauses (~1 second), so there's nothing to tap per question.
2. Speech-to-text: Groq `whisper-large-v3-turbo`.
3. Two answers start at the same moment:
   - **Quick** (resume-based) streams in within about a second.
   - **Web-checked** (Groq `groq/compound`, which has built-in web search) appears below when ready, a few seconds later. It never moves the quick answer.
4. A new question cancels the old answer, so you always see the latest.

## Setup (one-time)
1. Free key at https://console.groq.com (no card).
2. Host this folder over HTTPS (needed for the mic on iPhone). Easiest: drag the folder onto https://app.netlify.com/drop, or use GitHub Pages / Cloudflare Pages.
3. On your iPhone open the link in **Safari** → Share → **Add to Home Screen**.
4. Open "Copilot" → ⚙︎ → paste the key, role, and resume text → Save → allow the microphone.
5. Tap **Start listening**. Screen is kept awake while it runs.

## Always listening
After you tap **Start listening** once, it never stops until you tap **Stop**. A watchdog checks every 2 seconds and reconnects the mic if iOS interrupts it (a call, Siri, a notification sound). The screen stays awake while it runs, so keep the app open in the foreground: iOS suspends the mic if you lock the phone or switch apps. Plug the phone in for long sessions.

## Notes
- iOS web apps can only hear the microphone, so the interviewer must be audible through your phone's mic (speakerphone or in-room).
- Free Groq limits are per organisation: roughly 30 requests/min, and about 250 web-search requests/day on `groq/compound`. If you see a rate-limit message, wait a few seconds.
- If a model name errors, edit it in ⚙︎ (Groq's model list changes).
- Key and resume are stored only in your phone's browser. Audio and text go only to Groq.
- Please check the interviewer's rules: many employers prohibit AI assistance during interviews.
