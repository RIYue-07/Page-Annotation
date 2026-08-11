---
name: product-design-router
description: Use when users invoke this plugin for a URL clone, an image- or screenshot-based frontend, or an annotated prototype change that needs the matching focused workflow.
---

# Product Design Router

This plugin bundles three focused prototype workflows. Route to the narrowest matching skill; this router does not build or annotate on its own.

## Routes

- For a faithful clone or recreation of a live URL, use [$url-to-code](../url-to-code/SKILL.md). Confirm the user owns the target or has permission to recreate it before capture.
- For a selected screenshot, mockup, Figma frame, or generated visual, use [$image-to-code](../image-to-code/SKILL.md). A written brief alone is not a selected visual target.
- For floating, element-anchored annotations in an existing HTML prototype, use [$annotation-mode](../annotation-mode/SKILL.md).

Before URL or image build work, load [$product-design-context](../product-design-context/SKILL.md) and run its preflight script. Use saved references only when relevant.

## Browser Choice

In Codex Desktop, use the in-app Browser first. Use Chrome only when the user asks for it, the task depends on an existing Chrome session, or the in-app browser is unavailable.

When a live URL cannot be captured in an approved browser, stop the URL-clone workflow and report the blocker. For image-based builds, do not start without the exact selected visual reference.
