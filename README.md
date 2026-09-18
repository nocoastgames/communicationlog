# Daily Communication Log

A single-page tool for writing daily home reports for special education students.
Tap what happened, optionally let Gemini tidy the teacher's note, and print a
one-page report or a colourful infographic.

Live at **https://nocoastgames.github.io/communicationlog/**

Everything lives in [`index.html`](index.html) — no build step, no server, no
account. GitHub Pages serves that file directly.

## How it works day to day

1. Add each student once with **+ Save to roster**. They become quick-pick chips.
2. Tap a chip to switch students. The dot shows where each one stands:
   grey = not started, amber = in progress, green = PDF saved.
3. Tap through the categories. Everything autosaves per student per date, so a
   refresh, a closed tab, or a dead battery never loses the day.
4. Write rough notes and hit **✨ Polish Notes** for a parent-ready paragraph,
   or **Translate** to flip it between English and Spanish.
5. **⬇️ Download Report** or **🎨 Download Infographic** saves a PDF straight to
   your downloads as `Daily_Report_<Name>_<date>.pdf`. Print from that file, and
   you keep a copy for your records.

## Carry-over between students

The class shares a schedule, so switching to a student who has no log yet brings
the previous student's **Worked on / Went to / Saw / Special events** along,
plus the **teacher's note** as a starting point to edit. A banner says what
carried, with **Start blank instead** to undo it.

A carried note is flagged — amber border plus *"Reused from the previous
student"* right above the download buttons — and stays flagged until you type
in it. It still describes the previous student until you change it.

**Mood, lunch, send-from-home and bathroom counts never carry.** Those are
per-child facts rather than a draft to reuse, and copying them would put wrong
information in a parent's hands.

Untick **Carry the day's activities and note over to the next student** to turn
the whole thing off.

## Customising the icons

Hit **✏️ Customize** to edit any category:

- **+ Add icon** opens a searchable bank of ~200 emoji grouped by area
  (Feelings, Learning, Places, People, Food, Care, Events, Activities, Marks).
  Give it a label and an optional Spanish label.
- The red **×** on a tile removes it. Built-in icons are only *hidden* — they
  come back as dashed ghost tiles while customising, tap to restore. Icons you
  created are deleted for good (with a confirmation).

Customisations are per-browser and persist across sessions.

## Gemini API key

The polish and translate features call `gemini-2.5-flash` directly from the
browser. Paste your key into the 🔑 dialog; it is stored in `localStorage` on
that device only and is never sent anywhere except Google. Get one free at
[aistudio.google.com/apikey](https://aistudio.google.com/apikey).

Everything except those two buttons works with no key at all.

## PDFs

The download buttons render the document off-screen at exactly 816px (8.5in at
96dpi) and rasterise it via html2pdf at 2× — roughly 192dpi, crisp in print.
Output is a single US Letter page, typically 100–200KB.

Both layouts are built with HTML tables rather than CSS grid or `column-count`,
because html2canvas measures tables exactly and gets the modern layout modes
wrong. Keep that in mind before restyling the print documents.

Pressing **Ctrl+P** on the page still works and produces a *vector* print of the
standard report — smaller and text-searchable, but it does not leave a file
behind. Turn on **Background graphics** in Chrome if you go that route.

## Local data

Stored in `localStorage` under the `dcl.*` keys — roster, drafts, printed marks,
custom icons, carry-over preference, language. Drafts older than 60 days are
pruned automatically.
Clearing site data resets the tool to defaults.

## Repo notes

`src/`, `vite.config.ts`, `tsconfig.json` and `package.json` are leftover
scaffolding from the original AI Studio export. Nothing references them —
`index.html` is completely self-contained — and they can be deleted.
