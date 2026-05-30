# CommWise Modal & Button Traps

## Trap 1 — Modal open/close pattern

### The problem

`.dds-overlay` uses two independent CSS mechanisms:
- `dds-hidden` → `display: none !important` (removes from layout)
- `visible` → `opacity: 1; visibility: visible` (animates in)

Both must be managed together. Using only one leaves the modal invisible.

### What does NOT work

- `overlay.classList.add('visible')` alone — modal stays `display:none` if `dds-hidden` is present
- `overlay.classList.remove('dds-hidden')` alone — modal is in the layout but `opacity:0 / visibility:hidden`
- Skipping the reflow (`void offsetWidth`) — CSS transition does not fire; modal appears without animation but may flicker or stay invisible depending on browser

### Pattern — open

```javascript
overlay.classList.remove('dds-hidden');
void overlay.offsetWidth;          // mandatory reflow — triggers CSS transition
overlay.classList.add('visible');
```

### Pattern — close

```javascript
overlay.classList.remove('visible');
void overlay.offsetWidth;          // optional on close, safe to include
overlay.classList.add('dds-hidden');
```

### Reference implementation

`DDS_NODE_UI.openModal` (SCRIPT 1750) — canonical example to copy.

### Dynamic modals

When creating a modal via `createElement`, initialise with both classes:

```javascript
overlay.className = 'dds-overlay dds-hidden';
document.body.appendChild(overlay);
```

Then open with the pattern above.

---

## Trap 2 — Disabled buttons invisible (CommWise visibility override)

### The problem

CommWise applies `visibility: hidden` on all disabled buttons via a high-specificity global rule. Class-level CSS overrides (e.g. `.dds-btn-ghost:disabled`) are insufficient — the platform rule wins.

### What does NOT work

- `.dds-btn-ghost:disabled { visibility: visible }` — too low specificity

### Fix

Target each affected button by ID, covering both normal and `:disabled` states:

```css
#dds-btn-save,
#dds-btn-save:disabled {
  visibility: visible !important;
  display: inline-flex !important;
}
```

Apply this pattern to every new nav or toolbar button that can be in a disabled state.

### Reference

`#dds-btn-save` in STYLE 300 — canonical example.

---

## Keywords
CommWise, modal, overlay, dds-hidden, visible, display, opacity, visibility, disabled, button, CSS, override, trap
