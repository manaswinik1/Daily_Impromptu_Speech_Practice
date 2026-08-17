# Daily Impromptu

A single-page web app for daily impromptu speech practice: spin for a topic, set a
prep timer, record and transcribe your speech, and get AI-coached feedback —
filler word tracking, structure and vocabulary scoring, a one-thing takeaway to
work on next, and a "word of the day" pulled from your own transcript.

Everything runs client-side. There's no backend, no build step, and no framework —
just one HTML file.

## Running it

### Option A — GitHub Pages (recommended)

This is the easiest way to get a real `https://` URL, which browsers require for
microphone access and live transcription to work reliably.

1. Push this repo to GitHub.
2. Go to **Settings → Pages** on the repo.
3. Under **Build and deployment**, set **Source** to "Deploy from a branch",
   pick the `main` branch and `/ (root)` folder, then save.
4. GitHub will publish the site at `https://<your-username>.github.io/<repo-name>/`
   within a minute or two.
5. Open that URL, go to **Settings** inside the app, and add your Anthropic API
   key (see below).

### Option B — run it locally

Opening `index.html` directly from disk (a `file://` URL) will work for basic use,
but Chrome and Safari both restrict microphone recording and speech-to-text on
`file://` pages. To avoid that, serve it over localhost instead:

```bash
git clone <this-repo-url>
cd <this-repo-folder>
python3 -m http.server 8000
```

Then open `http://localhost:8000/` in Chrome or Edge (best support for live
transcription).

## Setting up your API key

The app calls the Anthropic API directly from your browser using **Claude Haiku**
(the cheapest current model) to score your speeches and power the "Ask a coach"
feature. It needs your own API key:

1. Get a key at [console.anthropic.com](https://console.anthropic.com) → API Keys.
2. In the app, open **Settings → Your Anthropic API key**, paste it in, and save.

Your key is stored only in your browser's local storage, on your own device, and
is sent directly from your browser to Anthropic's API for each request — never to
any other server. Real daily use (one speech plus a few coach questions) costs a
few cents a month on Haiku pricing.

If no key is set, the app still works using local, rule-based scoring (filler
counts, pacing, rough sentence-structure checks) as a fallback — just without the
AI-written feedback, varied coaching advice, or "Ask a coach" answers.

## What it does

- **Topic** — pick a level (Beginner/Intermediate/Advanced) and subjects once;
  every day it spins a fresh topic from those subjects.
- **Prep** — a draggable dial timer (30 sec–20 min) with quick presets; the topic
  stays visible the whole time so you can actually read it while you think.
- **Speak** — records audio and live-transcribes it (Chrome/Edge), with a running
  filler-word tracker and pacing readout.
- **Analysis** — a rating, a factual "how you did" writeup, one specific
  improvement to focus on next (never repeats a recent one), a vocabulary word
  drawn from your own speech, and a full score breakdown.
- **Ask a coach** — available while choosing a topic, while speaking, and after
  your analysis, with speech-specific suggested questions.
- **Guide** — speech structures (PREP, STAR, Rule of Three, etc.) and a
  cheat-sheet mapping topic phrasing to the right structure.
- **Progress** — streaks, rating and filler trends over time, and every vocab
  word you've collected.

## Data & privacy

All your data — sessions, ratings, transcripts, vocab words, and your API key —
is stored in your browser's `localStorage`, on your device only. Nothing is sent
anywhere except your own requests straight to Anthropic's API. Audio recordings
are the one exception: they only exist in memory for the current browser tab, so
they're lost on refresh — download a clip from its player if you want to keep it.

## License

MIT — see [LICENSE](LICENSE).
