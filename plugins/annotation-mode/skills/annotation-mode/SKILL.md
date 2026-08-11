---
name: annotation-mode
description: Use when users request 界面标注, 原型批注, 页面标记, or 标注.
---

# Annotation Mode

Add a review layer to an existing HTML prototype without changing product behavior when the mode is off.

## Workflow

1. Inspect page entry points, event delegation, responsive CSS, storage keys, and tests before editing.
2. Add failing regression tests for requested behavior, then establish the existing smoke-suite baseline.
3. Create one fixed-position, accessible floating controller outside normal document flow. Keep it visible on the page; only its explicit `开启批注模式` toggle enters annotation mode.
4. Keep annotation state separate from product state. Use a versioned key, parse and validate JSON, and tolerate unavailable or malformed storage.
5. In annotation mode, target only visible user-facing elements. Exclude the controller, markers/editors, `script`, `style`, hidden nodes, and disabled chrome unless requested.
6. Build selectors in this order: stable ID/data attribute; stable ancestor path scoped to the visible page region; short `:nth-of-type` disambiguator. Never rely on dynamic classes, text alone, or a global index.
7. Clicking a target opens an editor. Reject empty descriptions inline; Escape cancels. Save `{ id, page, view, selector, label, description, createdAt, updatedAt }`.
8. Render markers in an overlay without changing document flow. Recalculate after render, scroll, resize, sidebar changes, and responsive layout changes. Locate actions scroll the target into view.
9. Support locate, copy, edit, and delete. Copy plain text includes page/view, target label, selector, and description. Stop annotation UI events from creating annotations.
10. When the toggle is off, remove outlines, markers, interception, and editor focus. On narrow screens, keep controller/editor within the visual viewport and safe-area insets; long lists and descriptions must scroll.
11. Run the complete suite and inspect desktop, narrow mobile, and rotated mobile renders. Report missing browser automation or stale-anchor behavior.

## Interaction Contract

- The floating controller is always available, but creation is impossible while the toggle is off.
- Mode on shows a non-blocking hover outline; clicking a target creates a draft editor.
- Mode off leaves product clicks and keyboard navigation unchanged.
- Duplicate target clicks create a new record unless the user explicitly chose edit.
- Delete removes the record from storage and the overlay.
- Resetting demo data must not delete annotations unless explicitly defined.

## Validation Checklist

- Tests cover toggle gating, create/save/cancel, reload persistence, malformed storage, copy/edit/delete, Escape, and stale anchors.
- Repeated cards, buttons, or labels resolve to the intended visible instance after rerender.
- Markers stay aligned after scroll, resize, layout changes, and viewport rotation.
- Desktop and mobile renders show no overlap with content, fixed navigation, or safe-area edges.
- No console errors, remote runtime dependency, unbounded selector, or unhandled `localStorage` exception is introduced.
