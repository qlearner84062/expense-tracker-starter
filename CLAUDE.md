# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Starter project for a Claude Code course (codewithmosh.com). A single-page expense/finance tracker built with React + Vite. It intentionally ships with a bug, poor UI, and messy code that get fixed incrementally during the course — don't "clean up" things that look wrong unless asked, since the mess is the point of the exercise.

## Commands

```bash
npm install     # install dependencies
npm run dev     # start Vite dev server at http://localhost:5173
npm run build   # production build
npm run preview # preview the production build
npm run lint    # run ESLint
```

There is no test suite configured in this repo.

## Architecture

This is an unstructured single-component app: all state and logic lives in `src/App.jsx`, with no sub-components, no routing, and no backend — everything is in-memory React `useState`.

- `src/main.jsx` mounts `<App />` into `#root` in StrictMode.
- `src/App.jsx` owns everything:
  - `transactions` state (seeded with hardcoded sample data) plus form state for a new transaction (`description`, `amount`, `type`, `category`) and filter state (`filterType`, `filterCategory`).
  - Income/expense/balance totals are derived by `reduce`-ing over `transactions` on every render — amounts are stored and summed as **strings**, not numbers (both the seed data and the `handleSubmit` input values), so arithmetic on them is string concatenation rather than addition. This is the known intentional bug referenced in the README.
  - Filtering is done by chaining `.filter()` on `transactions` based on the two filter selects.
  - Everything (summary cards, add-transaction form, filters, transactions table) is rendered inline in one JSX return — there are no extracted subcomponents.
- Styling is plain CSS in `src/App.css` / `src/index.css`, no CSS framework.
