# ⇅ Sort by Label — Trello Power-Up

![Sort by Label icon](sort-by-label-icon.svg)

A lightweight Trello Power-Up that lets you sort cards within any list by their label — alphabetically, reverse, or with unlabeled cards first. The popup automatically adapts its color theme to match whatever background is set on the board it's loaded into.

---

## Features

- **Sort any list** by label name (A → Z, Z → A, or unlabeled first)
- **Adaptive theming** — the popup reads the board's background colors and renders a matching gradient UI
- **No backend required** — 100% static HTML/JS, hostable on GitHub Pages
- **Secondary sort** — cards with the same label are sub-sorted alphabetically by card name for a consistent, deterministic order

---

## Preview

The popup UI rendered on a dark blue "Mind Like Water" GTD board:

> The sort button appears in the board toolbar as **⇅ Sort by Label**. Clicking it opens a styled popup where you choose a list and sort direction, then hit Sort Cards.

---

## Files

| File | Purpose |
|------|---------|
| `index.html` | Connector file — loaded as a hidden iframe by Trello to register the Power-Up capabilities |
| `sort-popup.html` | The visible popup UI — list selector, sort options, and sort button |

---

## Setup & Deployment

### 1. Fork or clone this repo

```bash
git clone https://github.com/ojaister/trello-sort-by-label.git
```

### 2. Enable GitHub Pages

1. Go to your repo → **Settings → Pages**
2. Under *Branch*, select `main` and click **Save**
3. Your connector URL will be:
   ```
   https://YOUR-USERNAME.github.io/trello-sort-by-label/index.html
   ```

### 3. Register the Power-Up in Trello

1. Go to [https://trello.com/power-ups/admin](https://trello.com/power-ups/admin)
2. Select the Workspace you want to add it to
3. Click **New** and fill in:
   - **Name**: Sort by Label
   - **Iframe connector URL**: your GitHub Pages URL from step 2
4. Click **Create**

### 4. Enable it on a board

1. Open any Trello board
2. Click **Power-Ups** in the board menu
3. Go to the **Custom** tab and enable **Sort by Label**
4. The **⇅ Sort by Label** button will appear in the board toolbar

---

## Usage

1. Click **⇅ Sort by Label** in the board toolbar
2. Choose the list you want to sort
3. Choose a sort direction:
   - **A → Z** — alphabetical by first label name
   - **Z → A** — reverse alphabetical
   - **Unlabeled first** — cards with no label float to the top
4. Click **Sort Cards**

Cards with no label sort to the bottom by default (unless *Unlabeled first* is selected). Cards sharing the same label are sub-sorted alphabetically by card name.

> **Note:** Trello will prompt for write authorization the first time you sort. This is required to reorder cards via the API.

---

## How It Works

The connector (`index.html`) reads the board's `backgroundTopColor`, `backgroundBottomColor`, and `backgroundBrightness` preferences from the Trello Power-Up API and passes them as URL parameters to the popup. The popup applies those values as CSS variables, rendering a gradient that mirrors the board's own visual theme — dark boards get a frosted-glass dark UI, light boards get a light-mode version automatically.

Card sorting happens entirely client-side. Once the order is determined, the Power-Up uses the Trello REST API to update each card's `pos` value sequentially.

---

## Requirements

- A Trello account (free tier works)
- Admin access to the Workspace where you want to install the Power-Up
- A public HTTPS host for the files (GitHub Pages is free and works perfectly)

---

## License

MIT — free to use, modify, and distribute.
