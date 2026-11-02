# Quick Look view

An embeddable native **QLPreviewView**, exposed as a View-based `QuickLookView`.
`Import quicklook`. This avoids the global QLPreviewPanel's responder-chain and
data-source ownership rules. No external viewer process or shell command is used.

Use the UI thread for construction, methods and final release. Keep the view
rooted in its owning window and call `Close` from that window's `Closed` handler.
`shouldCloseWithWindow` is disabled so the wrapper owns a single, explicit closing
path. Movie previews do not autoplay. Quick Look loads asynchronously; unsupported
file formats, sandbox permissions and preview-provider availability are native
platform behavior. This API does not promise rendered success or expose completion
callbacks. It does not grant sandbox access; hold a bookmark/security scope as
needed for the preview's whole lifetime.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add quicklook --git https://github.com/BuoyBay/quicklook.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
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

## Platform and scope

Quick Look is a macOS integration. Present previews through the documented native application context and lifetime.

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer quicklook
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
