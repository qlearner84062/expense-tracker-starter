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

No routing, no backend — everything is in-memory React `useState`. `src/main.jsx` mounts `<App />` into `#root` in StrictMode.

`App.jsx` is the top-level container and owns only:
- `transactions` state, seeded with hardcoded sample data (`amount` is a `number`).
- the `categories` list.
- `handleAddTransaction`, which appends a new transaction and is passed down to `TransactionForm`.

It composes three child components, each owning the state relevant to its job:
- `src/Summary.jsx` — takes `transactions` as a prop and derives `totalIncome`/`totalExpenses`/`balance` via `reduce`, rendering the three summary cards.
- `src/TransactionForm.jsx` — owns the new-transaction form state (`description`, `amount`, `type`, `category`); on submit it builds the transaction object (converting `amount` to a `Number`) and calls `onAddTransaction` prop rather than mutating state itself.
- `src/TransactionList.jsx` — owns the filter state (`filterType`, `filterCategory`), filters the `transactions` prop, and renders the filters UI + transactions table.

Styling is plain CSS in `src/App.css` / `src/index.css`, no CSS framework.
