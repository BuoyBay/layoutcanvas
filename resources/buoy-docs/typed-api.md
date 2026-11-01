---
title: "layoutcanvas typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["LCGRect", "LCWBitmapInfo", "LCWColumn", "LCWCommonControls", "LCWDate", "LCWTabItem", "LayoutEditor", "LayoutEditorCommandObserver", "LayoutEditorHost", "LayoutNativeControlPainter", "LayoutNativeControlSpec", "LayoutNativePoint", "LayoutNativeRect", "LayoutNativeSize", "LayoutWheelCanvas", "LayoutWheelPoint"]
dependencies: []
symbols: ["LCGRect", "LCWBitmapInfo", "LCWColumn", "LCWCommonControls", "LCWDate", "LCWTabItem", "LayoutEditor", "LayoutEditorCommandObserver", "LayoutEditorHost", "LayoutNativeControlPainter", "LayoutNativeControlSpec", "LayoutNativePoint", "LayoutNativeRect", "LayoutNativeSize", "LayoutWheelCanvas", "LayoutWheelPoint"]
related: ["api.md", "getting-started.md", "index.md"]
---

# layoutcanvas typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## LayoutEditorHost

`Public Interface LayoutEditorHost`

The application owns the authoritative document, transactions and undo history.

### CommitLayoutEdits

`Function CommitLayoutEdits(expectedVersion As Integer, edits As Array Of EditorEdit) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `expectedVersion` | `Integer` | `ByVal` | Required |
| `edits` | `Array Of EditorEdit` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### LayoutSelectionChanged

`Sub LayoutSelectionChanged(nodeId As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `nodeId` | `String` | `ByVal` | Required |

Returns: no value.

### LayoutStatus

`Sub LayoutStatus(message As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `message` | `String` | `ByVal` | Required |

Returns: no value.

## LayoutEditorCommandObserver

`Public Interface LayoutEditorCommandObserver`

Optional: a host that also implements this is told whenever selection, document, viewport or toggle state changes so it can refresh menus and toolbars.

### LayoutCommandStateChanged

`Sub LayoutCommandStateChanged()`

No parameters.

Returns: no value.

## LayoutEditor

`Public Partial Class LayoutEditor Inherits View`

Native composite; draws representations only and never instantiates source controls. The class is split into Partial fragments: this core (document, selection, host and model commands), LayoutCanvasStage, LayoutCanvasInspector and LayoutCanvasPalette.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `PanelSplitter` | `Splitter` | Yes | No | — | Native divider controls around the design surface. Sidebar widths survive relayout. |
| `PaletteWidth` | `Integer` | No | No | — | — |
| `ChromeAppearance` | `String` | No | No | — | Appearance of the inspector and palette panels: "auto" (default) follows the application's effective appearance so painted panels always match their native child controls; "light"/"dark" force it. Independent of CanvasAppearance, which only previews the designed layout. |
| `ChromeDark` | `Boolean` | Yes | No | — | — |
| `Catalog` | `LayoutCatalog` | No | No | — | — |
| `ActiveRootId` | `String` | Yes | No | — | — |
| `SelectedId` | `String` | Yes | No | — | — |
| `RefactorAvailable` | `Boolean` | Yes | No | — | — |
| `ConstraintsSupported` | `Boolean` | Yes | No | — | — |
| `AlignTarget` | `String` | No | No | — | The alignment reference used by the align-* commands: selection, key or parent. |
| `CustomViewCount` | `Integer` | Yes | No | — | — |
| `InspectorExpression` | `String` | Yes | No | — | — |
| `InspectorReadOnly` | `Boolean` | Yes | No | — | — |
| `ActiveInspectorRow` | `String` | Yes | No | — | Key of the active inspector row ("name", "x", "prop:Caption", ...). |
| `InspectorEditorText` | `String` | Yes | No | — | Text currently shown in the overlaid value editor ("" when hidden). |
| `InspectorFilter` | `String` | No | No | — | — |
| `InspectorVisible` | `Boolean` | No | No | — | — |
| `InspectorWidth` | `Integer` | No | No | — | — |
| `InspectorMode` | `String` | No | No | — | — |
| `InspectorScrollOffset` | `Integer` | Yes | No | — | — |
| `PaletteScrollOffset` | `Double` | Yes | No | — | — |
| `PaletteFilter` | `String` | No | No | — | Search text; matches display name, type, category, package and description. |
| `PaletteGridMode` | `Boolean` | No | No | — | Icon grid (True) or icon + name list (False). |
| `PaletteVisible` | `Boolean` | No | No | — | Whether the palette column is shown; hiding gives its width to the canvas. |
| `GuideTolerance` | `Double` | No | No | `4.0` | Snap tolerance for smart guides in screen pixels. |
| `GuideMargin` | `Integer` | No | No | `20` | Parent inset offered as an extra smart-guide target (layout units). |
| `FitOnLoad` | `Boolean` | No | No | `False` | When True, loading a document (or switching roots) fits the root into view. |
| `RelationTolerance` | `Integer` | No | No | `0` | — |
| `RelationMargins` | `Array Of Integer` | No | No | `[]` | — |
| `RelationSpacing` | `Array Of Integer` | No | No | `[]` | — |
| `RelationGuides` | `JSONItem` | No | No | `JSONItem.NewArray()` | — |
| `GridSize` | `Integer` | No | No | — | Grid spacing in layout units (0 = default 10). Setting a size above 1 also turns snap-to-grid on; 0 or 1 turns it off. |
| `ShowGrid` | `Boolean` | No | No | — | — |
| `SnapToGrid` | `Boolean` | No | No | — | — |
| `SmartGuides` | `Boolean` | No | No | — | — |
| `ShowBounds` | `Boolean` | No | No | — | — |
| `ShowSpacing` | `Boolean` | No | No | — | — |
| `CanvasAppearance` | `String` | No | No | — | — |
| `NativeControlRendering` | `Boolean` | No | No | — | When True (default) builtin controls are drawn by the OS where supported (macOS, Windows and GTK4); False forces the portable canvas approximations everywhere. |
| `NativeControlRenderingSupported` | `Boolean` | Yes | No | — | True when this build has OS control drawing for the design canvas. |
| `NativeRenderingError` | `String` | Yes | No | — | — |
| `EffectiveCanvasAppearance` | `String` | Yes | No | — | — |
| `GestureActive` | `Boolean` | Yes | No | — | — |
| `MarqueeActive` | `Boolean` | Yes | No | — | — |
| `SmartGuideCount` | `Integer` | Yes | No | — | Number of smart-guide lines currently shown (live during gestures). |
| `SpacingMarkerCount` | `Integer` | Yes | No | — | Number of spacing markers currently shown. |
| `Zoom` | `Double` | Yes | No | — | — |
| `PanX` | `Double` | Yes | No | — | — |
| `PanY` | `Double` | Yes | No | — | — |
| `PreviewX` | `Integer` | Yes | No | — | — |
| `PreviewY` | `Integer` | Yes | No | — | — |
| `PreviewWidth` | `Integer` | Yes | No | — | — |
| `PreviewHeight` | `Integer` | Yes | No | — | — |
| `NativeInputError` | `String` | Yes | No | — | — |
| `PlacementArmed` | `Boolean` | Yes | No | — | — |

### Constructor

`Public Sub Constructor()`

No parameters.

Returns: no value.

### LayoutPanel

`Public Sub LayoutPanel(width As Integer, height As Integer)`

Columns: optional palette &#124; native divider &#124; canvas &#124; native divider &#124; inspector.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `width` | `Integer` | `ByVal` | Required |
| `height` | `Integer` | `ByVal` | Required |

Returns: no value.

### LayoutSplitContents

`Public Sub LayoutSplitContents()`

Native pane resize callbacks lay out children in their own pane coordinates.

No parameters.

Returns: no value.

### RememberPanelWidths

`Public Sub RememberPanelWidths()`

Store only user divider changes, so a narrow window does not erase preferences.

No parameters.

Returns: no value.

### RelayoutPanel

`Public Sub RelayoutPanel()`

Re-applies the last LayoutPanel size after a fragment changes its column width.

No parameters.

Returns: no value.

### SelectRootIndex

`Public Sub SelectRootIndex(index As Integer)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `index` | `Integer` | `ByVal` | Required |

Returns: no value.

### SelectRoot

`Public Function SelectRoot(id As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `id` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### AttachHost

`Public Sub AttachHost(host As LayoutEditorHost)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `host` | `LayoutEditorHost` | `ByVal` | Required |

Returns: no value.

### DetachHost

`Public Sub DetachHost()`

No parameters.

Returns: no value.

### LoadDocument

`Public Sub LoadDocument(document As LayoutDocument)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `document` | `LayoutDocument` | `ByVal` | Required |

Returns: no value.

### SelectNode

`Public Sub SelectNode(id As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `id` | `String` | `ByVal` | Required |

Returns: no value.

### SelectNodes

`Public Sub SelectNodes(ids As Array Of String)`

Replaces the selection. The first valid id becomes the key (primary) object. Unknown ids, ids outside the active root, duplicates and descendants of other selected nodes are dropped.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `ids` | `Array Of String` | `ByVal` | Required |

Returns: no value.

### SelectedIds

`Public Function SelectedIds() As Array Of String`

Primary (key) object first.

No parameters.

#### Returns

| Type |
| --- |
| `Array Of String` |

### InsertControl

`Public Function InsertControl(parentId As String, typeName As String, controlName As String, x As Integer, y As Integer, width As Integer, height As Integer) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `parentId` | `String` | `ByVal` | Required |
| `typeName` | `String` | `ByVal` | Required |
| `controlName` | `String` | `ByVal` | Required |
| `x` | `Integer` | `ByVal` | Required |
| `y` | `Integer` | `ByVal` | Required |
| `width` | `Integer` | `ByVal` | Required |
| `height` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### RenameSelected

`Public Function RenameSelected(newName As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `newName` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### DeleteSelected

`Public Function DeleteSelected() As Boolean`

Deletes every selected control through the project refactor host, one project-safe transaction per control (re-found by name after each reload).

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### Constraints

`Public Function Constraints() As JSONItem`

No parameters.

#### Returns

| Type |
| --- |
| `JSONItem` |

### AddConstraint

`Public Function AddConstraint(leftNodeId As String, leftAnchor As String, relation As String, rightNodeId As String, rightAnchor As String, offset As Integer, priority As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `leftNodeId` | `String` | `ByVal` | Required |
| `leftAnchor` | `String` | `ByVal` | Required |
| `relation` | `String` | `ByVal` | Required |
| `rightNodeId` | `String` | `ByVal` | Required |
| `rightAnchor` | `String` | `ByVal` | Required |
| `offset` | `Integer` | `ByVal` | Required |
| `priority` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### EditConstraint

`Public Function EditConstraint(constraintId As String, leftNodeId As String, leftAnchor As String, relation As String, rightNodeId As String, rightAnchor As String, offset As Integer, priority As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `constraintId` | `String` | `ByVal` | Required |
| `leftNodeId` | `String` | `ByVal` | Required |
| `leftAnchor` | `String` | `ByVal` | Required |
| `relation` | `String` | `ByVal` | Required |
| `rightNodeId` | `String` | `ByVal` | Required |
| `rightAnchor` | `String` | `ByVal` | Required |
| `offset` | `Integer` | `ByVal` | Required |
| `priority` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### DeleteConstraint

`Public Function DeleteConstraint(constraintId As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `constraintId` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### RefreshCatalog

`Public Sub RefreshCatalog()`

No parameters.

Returns: no value.

### ApplyFrame

`Public Function ApplyFrame(x As Integer, y As Integer, width As Integer, height As Integer) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `x` | `Integer` | `ByVal` | Required |
| `y` | `Integer` | `ByVal` | Required |
| `width` | `Integer` | `ByVal` | Required |
| `height` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### AlignNodes

`Public Function AlignNodes(nodeIds As Array Of String, mode As String) As Boolean`

Hosts may provide their own multi-selection UI; each command is one undo transaction. The first id is the alignment reference.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `nodeIds` | `Array Of String` | `ByVal` | Required |
| `mode` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### DistributeNodes

`Public Function DistributeNodes(nodeIds As Array Of String, axis As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `nodeIds` | `Array Of String` | `ByVal` | Required |
| `axis` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### PerformCommand

`Public Function PerformCommand(command As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `command` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### CanPerformCommand

`Public Function CanPerformCommand(command As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `command` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### CommandChecked

`Public Function CommandChecked(command As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `command` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### BuildContextMenu

`Public Sub BuildContextMenu(base As MenuItem, screenX As Double, screenY As Double)`

Builds the surface's contextual menu for a surface-local point. Right-click on a control selects it first unless it is already selected.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `base` | `MenuItem` | `ByVal` | Required |
| `screenX` | `Double` | `ByVal` | Required |
| `screenY` | `Double` | `ByVal` | Required |

Returns: no value.

### ContextMenuChosen

`Public Sub ContextMenuChosen(tag As String)`

Contextual-menu choice (the item Tag is a command name or insert:Type).

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `tag` | `String` | `ByVal` | Required |

Returns: no value.

### ApplyGeometryFields

`Public Sub ApplyGeometryFields()`

Commits the active geometry row's editor (legacy "Apply frame").

No parameters.

Returns: no value.

### SelectProperty

`Public Function SelectProperty(name As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### InspectorRows

`Public Function InspectorRows() As JSONItem`

Visible inspector rows as JSON objects (key, kind, section, label, value, editor, kindName, mixed, checked, present, active, detail, options, commands).

No parameters.

#### Returns

| Type |
| --- |
| `JSONItem` |

### InspectorSectionCollapsed

`Public Function InspectorSectionCollapsed(name As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### ToggleInspectorSection

`Public Function ToggleInspectorSection(name As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### ActivateInspectorRow

`Public Function ActivateInspectorRow(key As String) As Boolean`

Makes a row active (property rows also bind custom/plugin editors).

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `key` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### CommitInspectorRow

`Public Function CommitInspectorRow(key As String, value As String) As Boolean`

Commits a value as if typed into the row's editor and confirmed with Return. Booleans take True/False; enums take an option expression or its short label.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `key` | `String` | `ByVal` | Required |
| `value` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### StepInspectorRow

`Public Function StepInspectorRow(key As String, delta As Integer) As Boolean`

Increments a numeric or geometry row by delta steps (arrow keys / stepper).

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `key` | `String` | `ByVal` | Required |
| `delta` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### EditPrimaryProperty

`Public Function EditPrimaryProperty() As Boolean`

Double-click behaviour: show Properties, select the primary text-like property and focus its editor. Returns whether an editor was focused.

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### SetInspectorModeIndex

`Public Sub SetInspectorModeIndex(index As Integer)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `index` | `Integer` | `ByVal` | Required |

Returns: no value.

### PerformAction

`Public Sub PerformAction(action As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `action` | `String` | `ByVal` | Required |

Returns: no value.

### ShowProperty

`Public Sub ShowProperty(index As Integer)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `index` | `Integer` | `ByVal` | Required |

Returns: no value.

### CommitBoundProperty

`Public Function CommitBoundProperty(nodeId As String, propertyName As String, version As Integer, generation As Integer, snapshot As LayoutDocument, expression As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `nodeId` | `String` | `ByVal` | Required |
| `propertyName` | `String` | `ByVal` | Required |
| `version` | `Integer` | `ByVal` | Required |
| `generation` | `Integer` | `ByVal` | Required |
| `snapshot` | `LayoutDocument` | `ByVal` | Required |
| `expression` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### ApplyPropertyField

`Public Sub ApplyPropertyField()`

Commits the active property's editor; opens the registered editor for plugin-backed properties.

No parameters.

Returns: no value.

### InspectorFieldKey

`Public Function InspectorFieldKey(purpose As String, key As KeyName, shift As Boolean) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `purpose` | `String` | `ByVal` | Required |
| `key` | `KeyName` | `ByVal` | Required |
| `shift` | `Boolean` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### InspectorFieldFinished

`Public Sub InspectorFieldFinished(purpose As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `purpose` | `String` | `ByVal` | Required |

Returns: no value.

### InspectorFieldChanged

`Public Sub InspectorFieldChanged(purpose As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `purpose` | `String` | `ByVal` | Required |

Returns: no value.

### InspectorPopupChanged

`Public Sub InspectorPopupChanged(purpose As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `purpose` | `String` | `ByVal` | Required |

Returns: no value.

### InspectorWheel

`Public Function InspectorWheel(dx As Double, dy As Double, pixels As Boolean) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `dx` | `Double` | `ByVal` | Required |
| `dy` | `Double` | `ByVal` | Required |
| `pixels` | `Boolean` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### InspectorGridMouseDown

`Public Sub InspectorGridMouseDown(x As Double, y As Double, clicks As Integer, secondary As Boolean)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `x` | `Double` | `ByVal` | Required |
| `y` | `Double` | `ByVal` | Required |
| `clicks` | `Integer` | `ByVal` | Required |
| `secondary` | `Boolean` | `ByVal` | Required |

Returns: no value.

### InspectorGridMouseDrag

`Public Sub InspectorGridMouseDrag(x As Double, y As Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `x` | `Double` | `ByVal` | Required |
| `y` | `Double` | `ByVal` | Required |

Returns: no value.

### InspectorGridMouseUp

`Public Sub InspectorGridMouseUp()`

No parameters.

Returns: no value.

### InspectorGridHover

`Public Sub InspectorGridHover(x As Double, y As Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `x` | `Double` | `ByVal` | Required |
| `y` | `Double` | `ByVal` | Required |

Returns: no value.

### InspectorGridKey

`Public Function InspectorGridKey(key As KeyName, shift As Boolean) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `key` | `KeyName` | `ByVal` | Required |
| `shift` | `Boolean` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### InspectorBackdropClick

`Public Sub InspectorBackdropClick(x As Double, y As Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `x` | `Double` | `ByVal` | Required |
| `y` | `Double` | `ByVal` | Required |

Returns: no value.

### InspectorPaintBackdrop

`Public Sub InspectorPaintBackdrop(g As Graphics)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `g` | `Graphics` | `ByVal` | Required |

Returns: no value.

### InspectorPaintGrid

`Public Sub InspectorPaintGrid(g As Graphics)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `g` | `Graphics` | `ByVal` | Required |

Returns: no value.

### InspectorPaintDetail

`Public Sub InspectorPaintDetail(g As Graphics)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `g` | `Graphics` | `ByVal` | Required |

Returns: no value.

### ShowConstraintAt

`Public Sub ShowConstraintAt(index As Integer)`

Selects a constraint for editing: 0 is a new constraint, n is the nth entry of Constraints().

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `index` | `Integer` | `ByVal` | Required |

Returns: no value.

### PaletteWheel

`Public Function PaletteWheel(dx As Double, dy As Double, pixels As Boolean) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `dx` | `Double` | `ByVal` | Required |
| `dy` | `Double` | `ByVal` | Required |
| `pixels` | `Boolean` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### SelectPaletteType

`Public Function SelectPaletteType(typeName As String) As Boolean`

Select by canonical catalog identity, including package-qualified controls. Unknown identities leave the current palette and placement state untouched. A known identity cancels any stale placement, clears a filter that hides it and expands its section.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `typeName` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### PaletteSelectedType

`Public Function PaletteSelectedType() As String`

The keyboard/selection item: the target of PerformAction("insert"/"arm").

No parameters.

#### Returns

| Type |
| --- |
| `String` |

### PaletteArmedType

`Public Function PaletteArmedType() As String`

The palette item armed for click placement, or "" when nothing is armed.

No parameters.

#### Returns

| Type |
| --- |
| `String` |

### PaletteVisibleTypes

`Public Function PaletteVisibleTypes() As Array Of String`

Item identities currently listed (filtered, collapsed sections omitted), in display order.

No parameters.

#### Returns

| Type |
| --- |
| `Array Of String` |

### PaletteSections

`Public Function PaletteSections() As Array Of String`

Section headers currently listed, in display order.

No parameters.

#### Returns

| Type |
| --- |
| `Array Of String` |

### PaletteCategoryCollapsed

`Public Function PaletteCategoryCollapsed(category As String) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `category` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### SetPaletteCategoryCollapsed

`Public Sub SetPaletteCategoryCollapsed(category As String, collapsed As Boolean)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `category` | `String` | `ByVal` | Required |
| `collapsed` | `Boolean` | `ByVal` | Required |

Returns: no value.

### PaletteItemFrame

`Public Function PaletteItemFrame(typeName As String) As JSONItem`

Scrolls a listed item into view and returns its frame in palette-canvas coordinates as {x, y, width, height}; an empty object when it is not listed (filtered out or in a collapsed section).

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `typeName` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `JSONItem` |

### PaletteSearchChanged

`Public Sub PaletteSearchChanged()`

No parameters.

Returns: no value.

### PaletteMouseDown

`Public Function PaletteMouseDown(x As Double, y As Double, clickCount As Integer) As Boolean`

Canvas-coordinate click. Returns True when the press hit an item.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `x` | `Double` | `ByVal` | Required |
| `y` | `Double` | `ByVal` | Required |
| `clickCount` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### PaletteMouseDrag

`Public Sub PaletteMouseDrag(x As Double, y As Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `x` | `Double` | `ByVal` | Required |
| `y` | `Double` | `ByVal` | Required |

Returns: no value.

### PaletteMouseUp

`Public Sub PaletteMouseUp(x As Double, y As Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `x` | `Double` | `ByVal` | Required |
| `y` | `Double` | `ByVal` | Required |

Returns: no value.

### PaletteMouseMove

`Public Sub PaletteMouseMove(x As Double, y As Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `x` | `Double` | `ByVal` | Required |
| `y` | `Double` | `ByVal` | Required |

Returns: no value.

### PaletteMouseExit

`Public Sub PaletteMouseExit()`

No parameters.

Returns: no value.

### PaletteKeyDown

`Public Function PaletteKeyDown(key As KeyName, character As Integer) As Boolean`

Keyboard navigation. Up/Down (and Left/Right in grid mode) move, PageUp/ PageDown/Home/End jump, Left/Right collapse/expand the section in list mode, Return inserts, Space arms, Escape disarms then clears the filter, printable characters and Backspace edit the filter. Returns True when handled.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `key` | `KeyName` | `ByVal` | Required |
| `character` | `Integer` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### PaintPalette

`Public Sub PaintPalette(g As Graphics, width As Double, height As Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `g` | `Graphics` | `ByVal` | Required |
| `width` | `Double` | `ByVal` | Required |
| `height` | `Double` | `ByVal` | Required |

Returns: no value.

### InvalidateNativeRendering

`Public Sub InvalidateNativeRendering()`

Drop native bitmap and failure caches after a host-specific appearance change.

No parameters.

Returns: no value.

### OpenInput

`Public Sub OpenInput()`

No parameters.

Returns: no value.

### CloseInput

`Public Sub CloseInput()`

No parameters.

Returns: no value.

### StageWheel

`Public Function StageWheel(dx As Double, dy As Double, pixels As Boolean) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `dx` | `Double` | `ByVal` | Required |
| `dy` | `Double` | `ByVal` | Required |
| `pixels` | `Boolean` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### SetViewport

`Public Sub SetViewport(zoom As Double, panX As Double, panY As Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `zoom` | `Double` | `ByVal` | Required |
| `panX` | `Double` | `ByVal` | Required |
| `panY` | `Double` | `ByVal` | Required |

Returns: no value.

### CursorAt

`Public Function CursorAt(screenX As Double, screenY As Double) As CursorType`

The cursor the surface shows over a screen point (also useful for tests).

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `screenX` | `Double` | `ByVal` | Required |
| `screenY` | `Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `CursorType` |

### BeginGesture

`Public Function BeginGesture(screenX As Double, screenY As Double, resize As Boolean = False) As Boolean`

Coordinates are canvas pixels. The document geometry is never changed by a gesture until it ends. Returns True when a move/resize gesture started. An explicit resize uses the bottom-right handle of the hit control.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `screenX` | `Double` | `ByVal` | Required |
| `screenY` | `Double` | `ByVal` | Required |
| `resize` | `Boolean` | `ByVal` | `False` |

#### Returns

| Type |
| --- |
| `Boolean` |

### PointerDown

`Public Function PointerDown(screenX As Double, screenY As Double, clickCount As Integer, shift As Boolean, option As Boolean, primary As Boolean, middle As Boolean = False) As Boolean`

Full pointer entry point used by the surface: Shift or Primary toggles a control in the selection, Option duplicates on drag, a second click edits or enters a container, and middle-button (or Space) drags pan.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `screenX` | `Double` | `ByVal` | Required |
| `screenY` | `Double` | `ByVal` | Required |
| `clickCount` | `Integer` | `ByVal` | Required |
| `shift` | `Boolean` | `ByVal` | Required |
| `option` | `Boolean` | `ByVal` | Required |
| `primary` | `Boolean` | `ByVal` | Required |
| `middle` | `Boolean` | `ByVal` | `False` |

#### Returns

| Type |
| --- |
| `Boolean` |

### UpdateGesture

`Public Sub UpdateGesture(screenX As Double, screenY As Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `screenX` | `Double` | `ByVal` | Required |
| `screenY` | `Double` | `ByVal` | Required |

Returns: no value.

### PointerDrag

`Public Sub PointerDrag(screenX As Double, screenY As Double, shift As Boolean, option As Boolean, primary As Boolean)`

Shift constrains (axis lock on move, aspect ratio on corner resize); Primary suppresses smart-guide and grid snapping.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `screenX` | `Double` | `ByVal` | Required |
| `screenY` | `Double` | `ByVal` | Required |
| `shift` | `Boolean` | `ByVal` | Required |
| `option` | `Boolean` | `ByVal` | Required |
| `primary` | `Boolean` | `ByVal` | Required |

Returns: no value.

### EndGesture

`Public Function EndGesture() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### PointerUp

`Public Function PointerUp() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### PointerMove

`Public Sub PointerMove(screenX As Double, screenY As Double)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `screenX` | `Double` | `ByVal` | Required |
| `screenY` | `Double` | `ByVal` | Required |

Returns: no value.

### PointerExited

`Public Sub PointerExited()`

No parameters.

Returns: no value.

### CancelGesture

`Public Sub CancelGesture()`

No parameters.

Returns: no value.

### KeyPressed

`Public Function KeyPressed(key As KeyName, character As Integer, shift As Boolean, option As Boolean, primary As Boolean) As Boolean`

Keyboard entry point used by the surface (also usable by hosts/tests). Returns True when the key was handled.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `key` | `KeyName` | `ByVal` | Required |
| `character` | `Integer` | `ByVal` | Required |
| `shift` | `Boolean` | `ByVal` | Required |
| `option` | `Boolean` | `ByVal` | Required |
| `primary` | `Boolean` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### KeyReleased

`Public Sub KeyReleased(key As KeyName)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `key` | `KeyName` | `ByVal` | Required |

Returns: no value.

### CommitPendingNudge

`Public Sub CommitPendingNudge()`

Timer callback; commits an accumulated keyboard nudge.

No parameters.

Returns: no value.

### RendererValuesFor

`Public Function RendererValuesFor(nodeId As String) As JSONItem`

Renderer context contains typed literal/default primitive keys. The reserved $expressions object contains EXACT source expressions for existing assignments only, including enums and unsupported expressions. Absence there means a typed key is a descriptor default preview. Nothing in this context is evaluated.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `nodeId` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `JSONItem` |

### PaintLayout

`Public Sub PaintLayout(g As Graphics)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `g` | `Graphics` | `ByVal` | Required |

Returns: no value.

### ArmPlacement

`Public Sub ArmPlacement(typeName As String, controlName As String)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `typeName` | `String` | `ByVal` | Required |
| `controlName` | `String` | `ByVal` | Required |

Returns: no value.

### DisarmPlacement

`Public Sub DisarmPlacement()`

No parameters.

Returns: no value.

## LayoutNativeControlSpec

`Public Class LayoutNativeControlSpec`

Platform-neutral description of one native control preview.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Kind` | `String` | No | No | `""` | Native kind ("" when the control has no OS-drawn chrome). |
| `Title` | `String` | No | No | `""` | — |
| `Text` | `String` | No | No | `""` | — |
| `Placeholder` | `String` | No | No | `""` | — |
| `State` | `Integer` | No | No | `0` | Button state: -1 mixed, 0 off, 1 on. |
| `Minimum` | `Double` | No | No | `0.0` | — |
| `Maximum` | `Double` | No | No | `100.0` | — |
| `Value` | `Double` | No | No | `0.0` | — |
| `Flag` | `Boolean` | No | No | `False` | Kind-specific switch: secure field, vertical slider or indeterminate bar. |
| `Elements` | `Integer` | No | No | `0` | NSDatePicker elements mask for the date kind. |
| `Items` | `Array Of String` | No | No | `[]` | — |
| `RowHeight` | `Double` | No | No | `24.0` | — |
| `Enabled` | `Boolean` | No | No | `True` | — |
| `FontName` | `String` | No | No | `""` | — |
| `FontSize` | `Double` | No | No | `0.0` | — |

### Key

`Public Function Key() As String`

No parameters.

#### Returns

| Type |
| --- |
| `String` |

## LayoutNativePoint

`Sequential Structure LayoutNativePoint`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `X` | `Double` | — | — |
| `Y` | `Double` | — | — |

## LayoutNativeSize

`Sequential Structure LayoutNativeSize`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `W` | `Double` | — | — |
| `H` | `Double` | — | — |

## LayoutNativeRect

`Sequential Structure LayoutNativeRect`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Origin` | `LayoutNativePoint` | — | — |
| `Size` | `LayoutNativeSize` | — | — |

## LayoutNativeControlPainter

`Public Class LayoutNativeControlPainter`

Paints builtin controls with the operating system's own control drawing.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Enabled` | `Boolean` | No | No | `True` | Hosts may turn OS drawing off to force the portable approximations. |
| `LastError` | `String` | No | No | `""` | Last native render failure ("" when none). |
| `BackingScaleFactor` | `Double` | No | No | `0.0` | — |

### Constants

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `CacheLimit` | `Integer` | `256` | Upper bound on cached snapshots before the cache is cleared wholesale. |
| `PixelLimit` | `Integer` | `16777216` | Upper bound on snapshot pixels (width x height) at any zoom. |

### Supported

`Public Shared Function Supported() As Boolean`

True when this build can ask the OS to draw controls.

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

### CachedCount

`Public Function CachedCount() As Integer`

No parameters.

#### Returns

| Type |
| --- |
| `Integer` |

### ClearCache

`Public Sub ClearCache()`

No parameters.

Returns: no value.

### RasterScale

`Public Shared Function RasterScale(zoom As Double, backing As Double, w As Double, h As Double) As Double`

Raster density for a snapshot: zoom times backing scale, rounded up to a quarter step (limits re-rendering while zooming), clamped to [1, 8] and reduced so rounded bitmap dimensions never exceed PixelLimit pixels. Zero requests the portable fallback when even quarter scale is too large.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `zoom` | `Double` | `ByVal` | Required |
| `backing` | `Double` | `ByVal` | Required |
| `w` | `Double` | `ByVal` | Required |
| `h` | `Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Double` |

### SpecFor

`Public Shared Function SpecFor(typeName As String, nodeName As String, values As JSONItem, h As Double) As LayoutNativeControlSpec`

Maps a builtin type and its renderer values (literal keys plus the exact $expressions object) to a native preview. Nothing is evaluated: enum and unsupported expressions are matched textually or use the default.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `typeName` | `String` | `ByVal` | Required |
| `nodeName` | `String` | `ByVal` | Required |
| `values` | `JSONItem` | `ByVal` | Required |
| `h` | `Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `LayoutNativeControlSpec` |

### CacheKey

`Public Shared Function CacheKey(spec As LayoutNativeControlSpec, w As Double, h As Double, dark As Boolean, scale As Double) As String`

Cache key: visual spec, exact logical size, appearance and raster density.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `spec` | `LayoutNativeControlSpec` | `ByVal` | Required |
| `w` | `Double` | `ByVal` | Required |
| `h` | `Double` | `ByVal` | Required |
| `dark` | `Boolean` | `ByVal` | Required |
| `scale` | `Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `String` |

### Snapshot

`Public Function Snapshot(typeName As String, nodeName As String, w As Double, h As Double, values As JSONItem, dark As Boolean, zoom As Double) As Picture`

OS-drawn snapshot for the control, from the cache when possible; Nil when this platform or control has no native drawing.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `typeName` | `String` | `ByVal` | Required |
| `nodeName` | `String` | `ByVal` | Required |
| `w` | `Double` | `ByVal` | Required |
| `h` | `Double` | `ByVal` | Required |
| `values` | `JSONItem` | `ByVal` | Required |
| `dark` | `Boolean` | `ByVal` | Required |
| `zoom` | `Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Picture` |

### PaintSegments

`Public Function PaintSegments(g As IGraphics, labels As Array Of String, selected As Integer, x As Double, y As Double, w As Double, h As Double, dark As Boolean, zoom As Double) As Boolean`

Draws an OS segmented control (equal segments, one selected) for host chrome such as mode switches. Returns False when the caller must paint its own; hit-testing stays with the caller.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `g` | `IGraphics` | `ByVal` | Required |
| `labels` | `Array Of String` | `ByVal` | Required |
| `selected` | `Integer` | `ByVal` | Required |
| `x` | `Double` | `ByVal` | Required |
| `y` | `Double` | `ByVal` | Required |
| `w` | `Double` | `ByVal` | Required |
| `h` | `Double` | `ByVal` | Required |
| `dark` | `Boolean` | `ByVal` | Required |
| `zoom` | `Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### Paint

`Public Function Paint(g As IGraphics, typeName As String, nodeName As String, x As Double, y As Double, w As Double, h As Double, values As JSONItem, dark As Boolean, zoom As Double) As Boolean`

Draws the OS rendering into (x, y, w, h) in the caller's coordinate space (zoom and clipping come from g). Returns False when the caller must paint its own approximation.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `g` | `IGraphics` | `ByVal` | Required |
| `typeName` | `String` | `ByVal` | Required |
| `nodeName` | `String` | `ByVal` | Required |
| `x` | `Double` | `ByVal` | Required |
| `y` | `Double` | `ByVal` | Required |
| `w` | `Double` | `ByVal` | Required |
| `h` | `Double` | `ByVal` | Required |
| `values` | `JSONItem` | `ByVal` | Required |
| `dark` | `Boolean` | `ByVal` | Required |
| `zoom` | `Double` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

## LCGRect

`Sequential Structure LCGRect`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `X` | `Single` | — | — |
| `Y` | `Single` | — | — |
| `W` | `Single` | — | — |
| `H` | `Single` | — | — |

## LCWBitmapInfo

`Sequential Structure LCWBitmapInfo`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Size` | `UInt32` | — | — |
| `Width` | `Int32` | — | — |
| `Height` | `Int32` | — | — |
| `Planes` | `UInt16` | — | — |
| `Bits` | `UInt16` | — | — |
| `Compression` | `UInt32` | — | — |
| `ImageSize` | `UInt32` | — | — |
| `XPels` | `Int32` | — | — |
| `YPels` | `Int32` | — | — |
| `Used` | `UInt32` | — | — |
| `Important` | `UInt32` | — | — |
| `Colors` | `UInt32` | — | — |

## LCWCommonControls

`Sequential Structure LCWCommonControls`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Size` | `UInt32` | — | — |
| `Classes` | `UInt32` | — | — |

## LCWTabItem

`Sequential Structure LCWTabItem`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Mask` | `UInt32` | — | — |
| `State` | `UInt32` | — | — |
| `StateMask` | `UInt32` | — | — |
| `Text` | `Ptr` | — | — |
| `TextMax` | `Int32` | — | — |
| `Image` | `Int32` | — | — |
| `Param` | `Int64` | — | — |

## LCWColumn

`Sequential Structure LCWColumn`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Mask` | `UInt32` | — | — |
| `Format` | `Int32` | — | — |
| `Width` | `Int32` | — | — |
| `Text` | `Ptr` | — | — |
| `TextMax` | `Int32` | — | — |
| `SubItem` | `Int32` | — | — |

## LCWDate

`Sequential Structure LCWDate`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `Year` | `UInt16` | — | — |
| `Month` | `UInt16` | — | — |
| `DayOfWeek` | `UInt16` | — | — |
| `Day` | `UInt16` | — | — |
| `Hour` | `UInt16` | — | — |
| `Minute` | `UInt16` | — | — |
| `Second` | `UInt16` | — | — |
| `Millisecond` | `UInt16` | — | — |

## LayoutWheelCanvas

`Public Class LayoutWheelCanvas Inherits Canvas`

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `LastWheelError` | `String` | No | No | `""` | — |

### NativeWheel

`Public Function NativeWheel(dx As Double, dy As Double, pixels As Boolean) As Boolean`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `dx` | `Double` | `ByVal` | Required |
| `dy` | `Double` | `ByVal` | Required |
| `pixels` | `Boolean` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

### OpenWheel

`Public Sub OpenWheel()`

No parameters.

Returns: no value.

### CloseWheel

`Public Sub CloseWheel()`

No parameters.

Returns: no value.

### WheelWidgetDestroyed

`Public Sub WheelWidgetDestroyed()`

No parameters.

Returns: no value.

### OwnsWheel

`Public Function OwnsWheel(window As Ptr, point As LayoutWheelPoint) As Boolean`

Availability: `#If TargetMac Then`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `window` | `Ptr` | `ByVal` | Required |
| `point` | `LayoutWheelPoint` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Boolean` |

## LayoutWheelPoint

`Sequential Structure LayoutWheelPoint`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `X` | `Double` | — | — |
| `Y` | `Double` | — | — |
