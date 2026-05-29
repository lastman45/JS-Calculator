# 🧮 Calculator

A clean, responsive web-based calculator built with vanilla HTML, CSS, and JavaScript. Features a modern dark-themed UI with teal accent operators and smooth neumorphic button styling.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [File Breakdown](#file-breakdown)
  - [Calculator.html](#calculatorhtml)
  - [Calculator.css](#calculatorcss)
  - [Calculator.js](#calculatorjs)
- [Design System](#design-system)
- [Known Issues & Limitations](#known-issues--limitations)
- [Potential Improvements](#potential-improvements)
- [Browser Compatibility](#browser-compatibility)

---

## Overview

This is a front-end-only calculator that performs basic arithmetic operations directly in the browser. It uses `eval()` to process expressions entered through the on-screen button interface. The UI is styled with a dark charcoal card on a light blue background, with neumorphic (soft shadow) button effects and teal-highlighted operator keys.

> **Note:** The project contains two implementations — an older commented-out version (div/button based) and the current active version (form/input based). Only the active version is described in this README.

---

## Features

- ✅ Basic arithmetic: addition (`+`), subtraction (`-`), multiplication (`*`), division (`/`)
- ✅ Decimal point input
- ✅ All Clear (`AC`) — resets the display instantly
- ✅ Delete (`DE`) — removes the last entered character (backspace)
- ✅ Double zero (`00`) shortcut for entering round numbers
- ✅ Live expression display with right-aligned text
- ✅ Responsive centered layout
- ✅ Neumorphic button shadows for a modern look
- ✅ Operator keys visually distinguished with teal (`#33ffd8`) color

---

## Project Structure

```
calculator/
│
├── Calculator.html      # App structure and button layout
├── Calculator.css       # All styling (active + commented legacy styles)
└── Calculator.js        # JavaScript logic (legacy functions, commented out)
```

---

## Getting Started

No build tools, frameworks, or dependencies are required.

### Prerequisites

- Any modern web browser (Chrome, Firefox, Edge, Safari)

### Running the Calculator

1. Clone or download the project files into a single folder.
2. Open `Calculator.html` in your browser:
   - Double-click the file in your file explorer, **or**
   - Drag it into an open browser window, **or**
   - Use a local server (e.g., VS Code Live Server extension):
     ```
     Right-click Calculator.html → Open with Live Server
     ```

That's it — no installation needed.

---

## Usage

| Button | Action |
|--------|--------|
| `0–9` | Appends the digit to the display |
| `00` | Appends double zero to the display |
| `.` | Appends a decimal point |
| `+` `-` `*` `/` | Appends the operator to the expression |
| `AC` | Clears the entire display |
| `DE` | Deletes the last character (backspace) |
| `=` | Evaluates the expression and shows the result |

**Example workflow:**
1. Press `7` → display shows `7`
2. Press `*` → display shows `7*`
3. Press `8` → display shows `7*8`
4. Press `=` → display shows `56`
5. Press `AC` → display clears to empty

---

## File Breakdown

### `Calculator.html`

The main document. Defines the page structure and wires up all button interactions inline via `onclick` attributes.

**Key structure:**
```
body
└── div.container          ← full-viewport centering wrapper
    └── div.calculator     ← dark card container
        └── form
            ├── div.display
            │   └── input[type=text][name=display]   ← the screen
            ├── div  (AC, DE, ., /)
            ├── div  (7, 8, 9, *)
            ├── div  (4, 5, 6, -)
            ├── div  (1, 2, 3, +)
            └── div  (00, 0, =)
```

**Notable implementation details:**
- All buttons are `<input type="button">` elements, not `<button>` tags.
- Button logic is written inline using `onclick` attributes.
- The display field is accessed via `display.value` — this works because form elements are accessible by their `name` attribute as properties of the `form` element, and the form is implicitly referenced in this context.
- The `=` button uses `eval(display.value)` to compute the result.

> ⚠️ The `<form>` tag wraps all inputs. Since there is no `action` or `submit` button, form submission is not triggered, but pressing Enter on some browsers may attempt to submit. See [Known Issues](#known-issues--limitations).

---

### `Calculator.css`

Contains two style blocks:

**1. Legacy styles (commented out):**
An earlier dark-themed design using `#calculator`, `#display`, and `#keys` IDs. Features circular buttons (`border-radius: 50px`), orange operator buttons (`hsl(35, 100%, 55%)`), and a large font size (`5rem`).

**2. Active styles:**
The current design uses these key rules:

| Selector | Purpose |
|----------|---------|
| `*` | Global reset — zero margin/padding, `box-sizing: border-box`, Poppins font |
| `.container` | Full-viewport flexbox centering, light blue (`#e3f9ff`) background |
| `.calculator` | Dark charcoal card (`#3a4452`), `border-radius: 10px`, `padding: 20px` |
| `.calculator form input` | Base button style — `60×60px`, rounded corners, transparent background, white text, neumorphic box-shadow |
| `form .display` | Right-aligns the display; uses `flex: 1` to stretch full width |
| `form .display input` | Large font (`45px`), no box-shadow, full-width text display |
| `form input.equal` | Wider button (`145px`) to fill the bottom row |
| `form input.operator` | Teal color (`#33ffd8`) for operator keys |

**Neumorphic shadow detail:**
```css
box-shadow:
  -8px -8px 15px rgba(255, 255, 255, 0.1),   /* top-left light */
   5px  5px 15px rgba(0, 0, 0, 0.2);          /* bottom-right dark */
```
This creates the illusion of buttons slightly raised off the dark surface.

---

### `Calculator.js`

Currently the JS file contains only **commented-out legacy code** from the earlier implementation. The active calculator requires no external JS — all logic is handled inline in the HTML.

**Legacy functions (commented out):**

```js
// appendToDisplay(input) — appends a character to the display
// clearDisplay()         — resets display to empty string
// calculate()            — evaluates the expression (note: contains a typo: `display.vlaue`)
```

> The legacy `calculate()` function has a typo: `display.vlaue = eval(...)` — `vlaue` instead of `value`. This would silently fail if uncommented.

---

## Design System

| Token | Value | Usage |
|-------|-------|-------|
| Background | `#e3f9ff` | Page background |
| Card | `#3a4452` | Calculator body |
| Button BG | `transparent` (on card) | All buttons |
| Text | `#ffffff` | Default button/display text |
| Operator accent | `#33ffd8` | Operator key labels |
| Font | `"Poppins", sans-serif` | All text |
| Button size | `60×60px` | Standard buttons |
| Equal button | `145px` wide | Bottom-row `=` key |
| Border radius | `10px` | Card and buttons |

---

## Known Issues & Limitations

| Issue | Detail |
|-------|--------|
| **`eval()` security** | Using `eval()` to compute expressions is a security risk in production environments. For a local/personal tool this is acceptable, but it should be replaced with a proper expression parser in any deployed context. |
| **No input validation** | Invalid expressions (e.g., `5//3`, `*4`) will cause `eval()` to throw an error, which is unhandled — the display will show `undefined` or break. |
| **No keyboard support** | The calculator cannot be operated with a physical keyboard. |
| **No negative number support** | There is no `+/-` toggle button for making numbers negative. |
| **Double decimal** | Nothing prevents entering `5.5.5`, which will produce an error on evaluation. |
| **Form Enter key** | Pressing Enter may try to submit the form in some browsers, clearing or reloading the display. |
| **`display.value` access pattern** | Accessing the display via `display.value` relies on implicit form element name resolution, which is fragile. Using `document.querySelector` would be more robust. |

---

## Potential Improvements

- [ ] **Replace `eval()`** with a safe math parser (e.g., [math.js](https://mathjs.org/)) to prevent errors and security issues
- [ ] **Add keyboard support** — map key presses to button actions
- [ ] **Error handling** — show a friendly `Error` message on invalid expressions instead of crashing
- [ ] **Input sanitisation** — prevent double operators, double decimals, leading operators
- [ ] **Percentage button** — add `%` operator
- [ ] **Positive/Negative toggle** — add `+/-` button
- [ ] **Calculation history** — show a small log of previous results above the display
- [ ] **Responsive/mobile sizing** — shrink buttons gracefully on small screens
- [ ] **Refactor JS out of HTML** — move all `onclick` logic into `Calculator.js` for cleaner separation of concerns
- [ ] **Accessibility** — add `aria-label` attributes to buttons and `role="application"` to the calculator wrapper

---

## Browser Compatibility

| Browser | Status |
|---------|--------|
| Chrome 90+ | ✅ Fully supported |
| Firefox 88+ | ✅ Fully supported |
| Edge 90+ | ✅ Fully supported |
| Safari 14+ | ✅ Fully supported |
| IE 11 | ❌ Not supported (no CSS variables, no modern flex support) |

---

*Built with plain HTML, CSS, and JavaScript — no frameworks, no dependencies.*
