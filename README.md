# Bankist

A minimalist browser-based banking application built with vanilla JavaScript. Developed as part of Jonas Schmedtmann's [The Complete JavaScript Course](https://www.udemy.com/course/the-complete-javascript-course/).

---

## Features

- **Authentication** — PIN-based login with per-account credentials
- **Transaction History** — Chronological movement display with relative date labels (Today, Yesterday, N days ago)
- **Fund Transfers** — Transfer balance between existing accounts
- **Loan Requests** — Approved when at least one deposit ≥ 10% of the requested amount; processed with a 2.5s delay
- **Account Closure** — Self-service account deletion with credential confirmation
- **Sort Transactions** — Toggle ascending sort on movements while keeping dates in sync
- **Auto Logout** — 2-minute inactivity timer, reset on any action
- **Internationalization** — Dates and currency formatted via the `Intl.DateTimeFormat` and `Intl.NumberFormat` APIs, respecting each account's locale and currency

---

## Tech Stack

| Layer    | Detail                                                                       |
| -------- | ---------------------------------------------------------------------------- |
| Language | Vanilla JavaScript (ES6+)                                                    |
| APIs     | Intl.DateTimeFormat, Intl.NumberFormat, setTimeout, setInterval              |
| Patterns | Array methods (map, filter, reduce, find, findIndex, some), DOM manipulation |
| Tooling  | None — no bundler, no dependencies                                           |

---

## Demo Accounts

| Username | PIN    | Currency           |
| -------- | ------ | ------------------ |
| `js`     | `1111` | EUR (pt-PT locale) |
| `jd`     | `2222` | USD (en-US locale) |

> Usernames are auto-generated from account owner initials.

---

## Project Structure

```
bankist/
├── index.html
├── style.css
└── script.js
```

All logic lives in `script.js`. No build step required — open `index.html` directly in a browser.

---

## Key Implementation Notes

- **Username generation** — derived at runtime by mapping owner name initials: `"Jonas Schmedtmann"` → `"js"`
- **Balance** — computed on every UI update via `reduce`, never stored statically
- **Interest** — calculated on deposits only; movements below €1/\$1 interest threshold are excluded
- **Sort stability** — movements are sorted by index mapping to keep `movementsDates` aligned with their corresponding transactions
- **Timer** — a single `setInterval` instance is tracked globally; cleared and restarted on login, transfer, and loan to prevent stacking

---

## Running Locally

```bash
git clone https://github.com/PrinceLemayian/bankist.git
cd bankist
# Open index.html in your browser — no server needed
open index.html   # macOS
start index.html  # Windows
```

---

## License

For educational purposes. Original design and course project by [Jonas Schmedtmann](https://github.com/jonasschmedtmann).
