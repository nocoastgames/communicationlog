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
   grey = not started, amber = in progress, green = printed.
3. Tap through the categories. Everything autosaves per student per date, so a
   refresh, a closed tab, or a dead battery never loses the day.
4. Write rough notes and hit **✨ Polish Notes** for a parent-ready paragraph,
   or **Translate** to flip it between English and Spanish.
5. **🖨️ Print Report** or **🎨 Print Infographic**, then choose *Save as PDF*.
   The filename is pre-filled as `Daily_Report_<Name>_<date>`.

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

## Printing

Reports are produced by the browser's own print pipeline, so PDFs are vector:
small, searchable, and selectable. Page setup is US Letter with 0.45" margins.
In Chrome's print dialog, turn **Background graphics** on for the infographic's
colour panels, and leave Headers and footers off.

## Local data

Stored in `localStorage` under the `dcl.*` keys — roster, drafts, printed marks,
custom icons, language. Drafts older than 60 days are pruned automatically.
Clearing site data resets the tool to defaults.

## Repo notes

`src/`, `vite.config.ts`, `tsconfig.json` and `package.json` are leftover
scaffolding from the original AI Studio export. Nothing references them —
`index.html` is completely self-contained — and they can be deleted.
