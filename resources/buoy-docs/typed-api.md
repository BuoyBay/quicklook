---
title: "quicklook typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["PreviewFrame", "QuickLookView"]
dependencies: []
symbols: ["PreviewFrame", "QuickLookView"]
related: ["api.md", "getting-started.md", "index.md"]
---

# quicklook typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## QuickLook functions

### QuickLookSupported

`Public Function QuickLookSupported() As Boolean`

No parameters.

#### Returns

| Type |
| --- |
| `Boolean` |

## PreviewFrame

`Sequential Structure PreviewFrame`

### Fields

| Name | Type | Value / Default | Description |
| --- | --- | --- | --- |
| `X` | `Double` | — | — |
| `Y` | `Double` | — | — |
| `Width` | `Double` | — | — |
| `Height` | `Double` | — | — |

## QuickLookView

`Public Class QuickLookView Inherits View`

Embed in your own window with AddSubview; use only on the UI thread.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `CurrentPath` | `String` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(compact As Boolean = False)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `compact` | `Boolean` | `ByVal` | `False` |

Returns: no value.

### Load

`Public Sub Load(file As FileSystemItem)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `file` | `FileSystemItem` | `ByVal` | Required |

Returns: no value.

### Clear

`Public Sub Clear()`

No parameters.

Returns: no value.

### Refresh

`Public Sub Refresh()`

No parameters.

Returns: no value.

### Close

`Public Sub Close()`

No parameters.

Returns: no value.

### Destructor

`Public Sub Destructor()`

No parameters.

Returns: no value.
