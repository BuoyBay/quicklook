---
title: "Quick Look"
summary: "Embed an owned native file preview in a desktop window."
category: "Overview"
order: 0
keywords: ["preview", "quick look", "files", "QLPreviewView"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# Quick Look

The `quicklook` package exposes an embedded macOS `QLPreviewView` as a Buoy `View`. It previews an existing local file inside your window rather than opening another application or taking over the global Quick Look panel. Construction creates an empty 320 by 240 container; movie previews do not autoplay.

## Platform support

macOS only. `QuickLookSupported()` returns False on Windows and Linux; constructing `QuickLookView` there throws. The package uses the system QuickLookUI framework.

## Ownership and lifetime

Construct, load, refresh, clear, and close on the UI thread. Keep the view rooted in its owning window and call `Close()` when that window closes. Closing is permanent and idempotent; loading or refreshing a closed view throws. `Clear()` removes the current item and can be called after close. Worker-thread destruction queues native cleanup to the main thread, so keep the application loop alive until cleanup drains.

## Read next

- [Getting started](getting-started.md)
- [API reference](api.md)
