---
title: "LayoutCanvas API"
summary: "Public APIs and lifecycle contracts for LayoutCanvas."
category: "Reference"
order: 20
keywords: ["canvas", "designer", "palette", "inspector", "geometry", "constraints"]
symbols: ["LayoutEditor", "LayoutEditorHost", "LayoutEditor.LoadDocument", "LayoutEditor.AttachHost", "LayoutEditor.DetachHost", "LayoutEditor.Catalog", "LayoutEditor.ActiveRootId", "LayoutEditor.SelectRoot", "LayoutEditor.BeginGesture", "LayoutEditor.ApplyFrame", "LayoutEditor.InsertControl", "LayoutEditor.SelectPaletteType", "LayoutEditor.InspectorMode", "LayoutEditor.Constraints", "LayoutEditor.RenameSelected", "LayoutEditor.DeleteSelected", "LayoutEditor.CanvasAppearance", "LayoutEditor.NativeControlRendering"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# LayoutCanvas API

## Hosting and navigation

| Symbol | Behavior |
| --- | --- |
| `LayoutEditor()` | Native View; construct and use on the UI thread. |
| `Catalog` | Descriptor and extension catalog; register builtins once. |
| `AttachHost(host)`, `DetachHost()` | Attach/expire the application’s edit and selection callbacks. |
| `LoadDocument(snapshot)` | Replace the inspected source snapshot. |
| `LayoutPanel(width, height)` | Lay out the native editor’s child controls. |
| `OpenInput()`, `CloseInput()` | Attach native wheel adapters when the host opens; detach before destroying its widgets. Both are safe to repeat. |
| `NativeInputError` | Native wheel adapter error message, or an empty string. |
| `PanelSplitter`, `PaletteWidth`, `InspectorWidth` | Native three-pane splitter and preferred side widths. User divider changes survive relayout and panel hide/show. |
| `ActiveRootId`, `SelectRoot(id)`, `SelectRootIndex(index)` | Choose a Window/View root from a multi-layout document. |
| `SelectedId`, `SelectNode(id)` | Snapshot-scoped node selection. |
| `SetViewport(zoom, panX, panY)` | Configure canvas navigation. |
| `CanvasAppearance`, `EffectiveCanvasAppearance` | Requested `auto`, `light`, or `dark` appearance and the effective mode. |
| `NativeControlRendering`, `NativeControlRenderingSupported` | OS-drawn builtin control previews (default `True`; macOS, Windows and GTK4) and whether this build supports them. `False` forces the portable approximations. |

| `InvalidateNativeRendering()` | Clear cached component images and failed render attempts, then repaint the canvas and Inspector. Use for host-specific appearance changes. |
| `NativeRenderingError` | Last native snapshot failure, or an empty string; unsupported/custom types use portable drawing. |

## Menus and toolbars

Use the same command name with `CanPerformCommand(command)` to refresh enabled state, `CommandChecked(command)` to refresh toggle state, and `PerformCommand(command)` when the user activates an item. Names are exact strings, such as `copy`, `paste`, `duplicate`, `align-left`, `zoom-fit`, `show-grid`, and `snap-to-grid`. Unknown names return False. A command being enabled does not guarantee its later execution succeeds: selection, clipboard contents, or the authoritative document can change before activation. Check the execution result and use the host’s `LayoutStatus(message)` callback for reported failures.

The host passed to `AttachHost` can also implement `LayoutEditorCommandObserver`. Its `LayoutCommandStateChanged()` callback signals that selection, document, viewport, or toggle state changed; query the command methods again to update menus and toolbars. Refresh once after attaching the host, and refresh clipboard-dependent commands when opening a menu because external clipboard changes do not generate this callback.

Geometry and property commands submit edit proposals through `LayoutEditorHost.CommitLayoutEdits`; the application still owns persistence and undo. Commands such as `delete` and `rename` also require the project refactor host described below.

## Geometry, properties, and palette

`BeginGesture`, `UpdateGesture`, `EndGesture`, and `CancelGesture` drive preview-and-commit gestures. `ApplyFrame`, `AlignNodes`, and `DistributeNodes` propose supported geometry changes. `GridSize`, `RelationTolerance`, `RelationMargins`, and `RelationSpacing` configure snapping; `RelationGuides` exposes the current guidance data.

`SelectProperty`, `InspectorExpression`, and `InspectorReadOnly` expose inspector state. Native property callbacks are bound to the selected node, snapshot revision, and selection generation. Do not retain a previous binding as an active editor callback.

`InspectorMode` chooses `properties`, `palette`, or `constraints`. `SelectPaletteType` uses canonical catalog identities and returns False for an unknown type without changing the choice. `InsertControl(parentId, typeName, controlName, x, y, width, height)` proposes an insertion. `ArmPlacement`, `DisarmPlacement`, and `PlacementArmed` control click-to-place. `RefreshCatalog` reloads palette choices.

## Constraints and refactors

`Constraints`, `ConstraintsSupported`, `AddConstraint`, `EditConstraint`, and `DeleteConstraint` support structured commands on Window roots. Standalone View roots cannot use compiler constraint lowering.

`RenameSelected`, `DeleteSelected`, and `RefactorAvailable` expose project commands. They require the host’s `LayoutProjectRefactorHost` implementation; the editor does not independently rewrite application references. `CustomViewCount` reports retained native property Views. Reusable factories avoid repeated allocation; legacy non-reusable factories have an allocation cap and then fall back to other editors.

## Continue reading

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)

[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
