---
title: "LayoutCanvas getting started"
summary: "Display a source document."
category: "Guides"
order: 10
keywords: ["canvas", "designer", "palette", "inspector", "geometry", "constraints"]
related: ["index.md", "api.md", "typed-api.md"]
---

# LayoutCanvas getting started

Install `layoutcanvas`, `layoutkit`, and `editorkit` in `packages/`. Import `layoutcanvas` and the explicit LayoutKit modules whose types the host uses.

The following complete program opens a source-preview surface. It deliberately attaches no mutation host, so it is a useful first inspection example rather than a persistence implementation. Construct native Views on the UI thread, size the editor with `Move` and `LayoutPanel`, then add it to a Window. Hosts should call `OpenInput()` in their window's Opening handler and `CloseInput()` before its native views are destroyed to enable wheel scrolling safely; see the repository's `examples/layout_designer_demo.bui` for that lifecycle wiring.

To enable edits, implement `LayoutEditorHost.CommitLayoutEdits(expectedVersion, edits)`, `LayoutSelectionChanged(nodeId)`, and `LayoutStatus(message)`. In the commit callback, reject stale revisions, update the authoritative EditorKit document once, and reload a new snapshot. A rejected proposal leaves source unchanged.

```buoy
Import layoutcanvas
Import layoutkit.LayoutDocument

Window DesignerHost
    Title = "Layout preview"
    Frame = (80, 80, 900, 600)
End Window

Sub Main()
    Dim host As New DesignerHost()
    Dim editor As New LayoutEditor()
    editor.Catalog.RegisterBuiltinControls()
    editor.Move(0.0, 0.0, 900.0, 600.0)
    editor.LayoutPanel(900, 600)
    host.AddSubview(editor)
    editor.LoadDocument(New LayoutDocument("Window Contact\n    Frame = (0, 0, 400, 240)\nEnd Window\n", 1))
    host.Show()
    Application.Run()
    editor.DetachHost()
End Sub
```

To connect an application menu or toolbar, use the command dispatcher and optional host observer described in [Menus and toolbars](api.md#menus-and-toolbars). Keep enabled and checked state in sync through the observer; route activation through `PerformCommand` so the same editor validation and host transaction path handles both menu and canvas actions.

In a workspace checkout, `tests/layoutcanvas_interaction_test.bui` provides a complete `ApplyHost` implementation with an authoritative `EditorDocument`, version checks, synchronous snapshot reload, project refactor callbacks, and command-state notifications. Its rejection cases illustrate why a host must return False when a proposal was not accepted. This repository test is not included in the installed package.

Register trusted extensions before loading source. Use `RefreshCatalog()` after catalog changes. Custom property Views should implement the reusable LayoutKit contract and replace old callback hosts on rebind. Unsupported or throwing factories fall back to available nonvisual/generic editors; they do not authorize stale callbacks.

## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
