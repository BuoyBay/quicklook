# Quick Look · 0.1.0

An embeddable native **QLPreviewView**, exposed as a Buoy `View` subclass.
`Import quicklook`. This avoids the global QLPreviewPanel's responder-chain and
data-source ownership rules. No external viewer process or shell command is used.

- `QuickLookSupported() As Boolean` reports platform support.
- `New QuickLookView(compact = False)` creates an empty 320×240 preview container.
- Move/anchor the view and add it to your own window using ordinary `AddSubview`.
- `Load(file As FileSystemItem)` accepts an existing local file. `CurrentPath` records the selected file; it is not a preview-completion signal.
- `Refresh()` regenerates the current preview; `Clear()` removes it.
- `Close()` permanently closes the native preview and is idempotent. Loading or refreshing a closed instance fails. The destructor also closes it.

Use the UI thread for construction, methods and final release. Keep the view
rooted in its owning window and call `Close` from that window's `Closed` handler.
`shouldCloseWithWindow` is disabled so the wrapper owns a single, explicit closing
path. Movie previews do not autoplay. Quick Look loads asynchronously; unsupported
file formats, sandbox permissions and preview-provider availability are native
platform behavior. This API does not promise rendered success or expose completion
callbacks. It does not grant sandbox access; hold a bookmark/security scope as
needed for the preview's whole lifetime.

macOS only. Windows/Linux report unsupported; construction throws. The bundled
linker stub describes Apple's system QuickLookUI framework; no third-party binary
is shipped.

Check rendered previews in the host application, with its actual sandbox
permissions and preview providers.

Apple API: [QLPreviewView](https://developer.apple.com/documentation/quicklookui/qlpreviewview).

Implicit teardown from a worker queues native cleanup to the main thread. Keep the application run loop alive until cleanup drains. Construction and all other UI operations remain main-thread-only.
