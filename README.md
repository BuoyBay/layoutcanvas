# Layout editor with Canvas inspector

A View-based native layout editor whose inspector, palette and stage surfaces inherit Canvas. `CanvasAppearance` defaults to `auto` and accepts `light` or `dark` for deterministic previews. Automatic appearance follows the OS and explicit GTK dark-theme selection. Builtin previews use contrasting text, field fills, borders and selection handles in both modes; package renderers receive `$appearance` alongside their typed values and `$expressions`. Constraint-controlled nested Views retain previews of their declared literal frames while direct dragging stays disabled; this is not a live constraint solver.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add layoutcanvas --git https://github.com/BuoyBay/layoutcanvas.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.
BPM also resolves `editorkit`, `layoutkit`, `controlsnapshot`.

## Example

```basic
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

## Build and API reference

Source is in `modules/`, with native/runtime inputs where required. Use the
[package guide](docs/API.md) for backend-specific build prerequisites, ownership
rules and supported targets. Rebuilding a native backend requires that target's
compiler and SDK; sealing an archive alone does not rebuild the backend.

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
