---
title: "Quick Look getting started"
summary: "Install quicklook and use its native API with explicit ownership."
category: "Guides"
order: 10
keywords: ["preview", "quick look", "files", "QLPreviewView"]
related: ["index.md", "api.md", "typed-api.md"]
---

# Getting started

Install `quicklook-0.1.0.buipkg` in your project’s `packages/` directory and import `quicklook`.

The helper below returns an owned preview for a file selected by the user. Call it on the UI thread, attach the returned view with your window’s normal `AddSubview` flow, and retain it until the window closes. Call `Close()` from the owning window’s close handler. The helper closes the preview if loading raises an exception.

```buoy
Import quicklook

Function CreateFilePreview(file As FileSystemItem) As QuickLookView
    If Not QuickLookSupported() Then Throw New UnsupportedOperationException("Quick Look requires macOS")
    Dim preview As New QuickLookView()
    Try
        preview.Load(file)
        Return preview
    Catch e As Exception
        preview.Close()
        Throw e
    End Try
End Function
```

## Handle native constraints

`Load` requires a non-Nil existing local file and rejects NUL in paths. `CurrentPath` records the selected path; it is not a completion signal. Preview generation is asynchronous, and provider availability, format support, and sandbox permissions affect the result. Hold any bookmark/security scope for the whole preview lifetime. This wrapper does not report successful rendering or grant access.

[Package overview](index.md) · [API reference](api.md)
