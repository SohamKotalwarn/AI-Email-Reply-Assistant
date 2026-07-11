# AI Email Reply Assistant

A single-file, client-side web app that generates draft email replies using rule-based keyword matching — no backend, no API keys, no data ever leaves your browser.

## Features

- **Modern dark UI** with a responsive two-pane layout (input / output) that stacks on mobile
- **Tone selector** — Formal, Friendly, Professional — each with its own greeting, closing line, and sign-off
- **Generate Reply** button that analyzes the pasted email and drafts a response
- **Copy Reply** button (clipboard API, with a manual-copy fallback)
- **Clear** button to reset both panes
- **Empty-input handling** — shows *"Please enter an email message to generate a reply."* if you click Generate with nothing typed
- Keyboard shortcut: `Ctrl+Enter` / `Cmd+Enter` inside the textarea also generates a reply

## How it works

This is **not** a connected AI model — it's a transparent, rule-based simulation of one, built entirely in JavaScript:

1. **`detectIntent(text)`** lowercases the pasted email and checks it against ordered keyword groups:
   - Meeting / scheduling
   - Complaint
   - Invoice / payment
   - Deadline / urgency
   - Apology
   - Request
   - Gratitude
   - Question (fallback: presence of `?`)
   - Generic (fallback if nothing else matches)
2. **`buildReplyBody(intent)`** returns a middle paragraph written for that detected intent.
3. **`toneStyle`** supplies the greeting, opening line, closing line, and sign-off for the selected tone.
4. **`generateReply()`** stitches these pieces together into the final reply shown in the output box.

Because matching is keyword-based, results are deterministic and easy to extend — see below.

## Getting started

No installation or build tools required.

1. Download `index.html`
2. Open it directly in any modern browser (Chrome, Firefox, Edge, Safari)

That's it — everything (HTML, CSS, JavaScript) lives in one file.

## Project structure

```
.
├── index.html   # Complete app: markup, styles, and logic in one file
└── README.md    # This file
```

## Customizing / extending

All logic lives inside the `<script>` block at the bottom of `index.html`.

- **Add a new intent category:** add an entry to the `rules` array in `detectIntent()` with an `intent` name and a `keywords` list, then add a matching entry in the `bodies` object inside `buildReplyBody()`.
- **Add a new tone:** add a new key to the `toneStyle` object (`greeting`, `opener`, `closerBeforeSignoff`, `signoff`) and a matching button in the HTML `.tone-row` with a `data-tone` attribute of the same name.
- **Change the visual theme:** colors, fonts, and spacing are controlled by CSS custom properties at the top of the `<style>` block under `:root`.

## Limitations

- This is a **rule-based** demo, not a large language model — it won't handle nuance, sarcasm, or intents outside the built-in keyword list as gracefully as a real AI would.
- Generated replies are drafts meant to be reviewed and personalized (e.g. replacing `[Your Name]`) before sending.

## License

Free to use, modify, and distribute for personal or commercial projects.
