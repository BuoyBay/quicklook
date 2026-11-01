---
title: "Quick Look API"
summary: "Public symbols and contracts for the quicklook package."
category: "Reference"
order: 20
keywords: ["preview", "quick look", "files", "QLPreviewView"]
symbols: ["QuickLookSupported", "QuickLookView", "QuickLookView.Load", "QuickLookView.CurrentPath", "QuickLookView.Refresh", "QuickLookView.Clear", "QuickLookView.Close"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# API reference

Import `quicklook` from the sealed package. The signatures below describe its public surface.

| Symbol | Contract |
| --- | --- |
| `QuickLookSupported() As Boolean` | Platform availability probe. |
| `New QuickLookView(compact As Boolean = False)` | Create an empty preview; compact selects the native compact style. |
| `CurrentPath As String` | Read-only path of the selected preview item; empty after Clear or Close. |
| `Load(file As FileSystemItem)` | Validate and assign the preview item. |
| `Refresh()` | Ask the native provider to regenerate the current preview. |
| `Clear()` | Remove the current preview item without permanently closing the view. |
| `Close()` | Permanently close and release the preview; repeated calls are safe. |

## Errors and lifecycle

`Load` requires a non-Nil existing local file and rejects NUL in paths. `CurrentPath` records the selected path; it is not a completion signal. Preview generation is asynchronous, and provider availability, format support, and sandbox permissions affect the result. Hold any bookmark/security scope for the whole preview lifetime. This wrapper does not report successful rendering or grant access.

Construct, load, refresh, clear, and close on the UI thread. Keep the view rooted in its owning window and call `Close()` when that window closes. Closing is permanent and idempotent; loading or refreshing a closed view throws. `Clear()` removes the current item and can be called after close. Worker-thread destruction queues native cleanup to the main thread, so keep the application loop alive until cleanup drains.

## Platform support

macOS only. `QuickLookSupported()` returns False on Windows and Linux; constructing `QuickLookView` there throws. The package uses the system QuickLookUI framework.

[Getting started](getting-started.md) · [Package overview](index.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
