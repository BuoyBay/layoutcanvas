---
title: "LayoutCanvas"
summary: "A native visual layout editor with revision-bound edit proposals and a source-preserving inspector."
category: "Overview"
order: 0
keywords: ["canvas", "designer", "palette", "inspector", "geometry", "constraints"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# LayoutCanvas

LayoutCanvas supplies `LayoutEditor Inherits View`, a native design surface built on LayoutKit snapshots and EditorKit edit batches. It paints approximations of controls rather than constructing the controls described by opened source.

The editor includes a canvas, root selection, a properties inspector, palette insertion/placement, and structured constraint editing. Supported literal geometry can be dragged or resized; gesture previews do not rewrite source. A completed gesture proposes one commit, allowing a single undo transaction.

## Host contract

The host owns the authoritative document, undo/redo, dirty state, persistence, and project refactors. Attach a `LayoutEditorHost`, compare expected revisions before committing edits, apply each batch atomically, and reload a fresh `LayoutDocument`. Call `DetachHost` during teardown. All native editor operations belong on the UI thread.

Nested plain Views preserve parent-relative coordinates. Unsupported container descendants and constraint-controlled frames remain read-only. The canvas displays declared geometry; it does not solve runtime layout constraints. Rename/delete commands require a host implementing `LayoutProjectRefactorHost` over the full project source closure.

## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
