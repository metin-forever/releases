# Client builds

Client builds for the test server, published by CI from the client repository. Each platform has a stable release that holds its newest build; the links below always serve it, and a build of one platform does not wait for the other. Each commit also has a release of its own, `client-<commit>`, holding the builds of that commit; only the newest few are kept.

| Platform | Download | Checksum |
|---|---|---|
| Windows | [metin-forever-client-windows.zip](https://github.com/metin-forever/releases/releases/download/client-windows-latest/metin-forever-client-windows.zip) | [.sha256](https://github.com/metin-forever/releases/releases/download/client-windows-latest/metin-forever-client-windows.zip.sha256) |
| macOS | [metin-forever-client-macos.zip](https://github.com/metin-forever/releases/releases/download/client-macos-latest/metin-forever-client-macos.zip) | [.sha256](https://github.com/metin-forever/releases/releases/download/client-macos-latest/metin-forever-client-macos.zip.sha256) |

## Version

Each build carries a version of the form `forever-YYYY.MM.DD.N`: the UTC date of its commit and the commit's position among that day's commits. The Windows and macOS builds of one commit have the same version. It is the title of every release (`forever-2026.10.25.3`) and appears in the notes, which also name the commit, and in the apps: on Windows under Properties → Details of `metin2client.exe`, on macOS under Get Info of `Forever.app`.

## Checking the download

Each zip has a `.sha256` file holding its SHA-256 checksum. On macOS or Linux, with both files in the same directory:

    shasum -a 256 -c metin-forever-client-macos.zip.sha256

On Windows, compute the checksum and compare it with the first field of the `.sha256` file:

    certutil -hashfile metin-forever-client-windows.zip SHA256

## Windows

Unpack the zip and start `metin2client.exe`; `config.exe` sets resolution and graphics options. The client uses the DirectX 9 runtime; if a `d3dx9` DLL is reported missing, install the DirectX End-User Runtime (June 2010).

The Windows client is not signed: on first start, Windows SmartScreen asks for confirmation under "More info".

## macOS

The macOS build runs on Apple Silicon Macs with macOS 14 or later; Intel Macs are not supported. The zip unpacks to a folder `Forever` holding `Forever.app` (the game) and `Forever Config.app` (resolution and graphics options).

Move the `Forever` folder to `/Applications` before the first launch. An app started from the download location runs from a temporary read-only copy (App Translocation), which macOS renews on each launch.

The apps are not signed with an Apple developer certificate, so macOS blocks the first launch. Either:

- try to open `Forever.app` once, then open System Settings → Privacy & Security and choose "Open Anyway" (repeat for `Forever Config.app`), or
- clear the quarantine flag on the folder in Terminal:

      xattr -dr com.apple.quarantine /Applications/Forever

Settings and logs are kept in `~/Library/Application Support/Forever/`, screenshots in `~/Pictures/Forever/`. Replacing the apps with a newer build leaves both in place.
