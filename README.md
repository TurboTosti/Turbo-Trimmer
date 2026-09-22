# TurboTrimmer

A portable trim-sheet editor for environment and game artists.

Build precise strip layouts, link textures to regions, and export sheets, masks and guides for Substance, Unreal Engine and Unity workflows.

**Current version: 0.1 alpha**

[Download releases](https://github.com/TurboTosti/Turbo-Trimmer/releases) | [Report an issue](https://github.com/TurboTosti/Turbo-Trimmer/issues)

## Choose an edition

| Edition | Platform | Browser runtime | Download |
| --- | --- | --- | --- |
| **TurboTrimmer** | Windows x64 | Included; no installed browser or WebView2 required | `TurboTrimmer-Portable-Windows-x64.zip` |
| **TurboTrimmer** | Linux x64 | Included; no installed browser required | `TurboTrimmer-Portable-Linux-x64.zip` |
| **TurboTrimmer Mini** | Windows x64 | Uses Microsoft WebView2 already installed on the computer | `TurboTrimmer-Portable-Mini-Windows-x64.zip` |

**TurboTrimmer** is the main edition. It uses Electron and includes Chromium and Node.js, making it suitable for a computer without a separately installed browser. The complete runtime travels with the application folder.

**TurboTrimmer Mini** is the smaller Windows edition, built with Tauri. It keeps the trim-sheet editing workflow while avoiding a bundled browser runtime. Choose Mini when WebView2 is already available and you prefer a smaller download. If WebView2 is missing, use the main Windows edition. Mini does not silently download or install a runtime.

Both editions use the same editable `.trim` project format. Shared editor fixes are maintained across both editions where applicable; individual release build numbers and platform behavior can differ. Mini is Windows-only.

## Features

- **Pixel-accurate layouts** - organize zones and strips, enter exact dimensions, and view measurements in pixels, percentages and UV coordinates.
- **Texture sets** - attach named texture paths to a strip and share tiling, scale, offset, rotation and filtering across them. Each strip acts as a mask.
- **Flexible exports** - export multiple named texture sheets with your own filename suffixes.
- **Production controls** - 8/16-bit texture PNG, 8-bit RGBA TGA, optional edge dilation and per-texture normal-map Y inversion.
- **Layout tools** - split, duplicate, arrange, lock and hide regions; use presets, snapping, guides, subdivisions and texel-density helpers.
- **Editable projects** - save and reopen projects with undo/redo and optional recovery.
- **Coverage checks** - find overlaps, gaps, invalid dimensions and regions outside their bounds.

## Get started

1. Open Releases and download the ZIP for your operating system and preferred edition.
2. Extract the complete ZIP into a writable folder.
3. On Windows, run `TurboTrimmer.exe` inside the extracted folder. The Mini executable may also use this filename.
4. On Linux, run `./TurboTrimmer` or `sh TurboTrimmer.sh` from its extracted folder.

Keep the application folder together. Do not copy only the executable. Leave `portable.flag` beside it so settings, presets, recovery files and browser data remain under `Data/`. The application uses no installer.

Windows releases target Windows 10/11 x64. Linux releases target Ubuntu 22.04 or newer and current Arch x64 desktops. The Linux edition still needs normal operating-system desktop libraries and Chromium sandbox support; it does not require an installed browser, Node.js or FUSE. Linux launch testing remains pending. See the build and testing notes included with the download for current platform limitations.

## A typical workflow

The editor starts with an empty sheet.

1. Create a sheet or load a layout preset.
2. Arrange zones and strips at your target texture resolution.
3. Select a strip and click **Texture Set** in Layers.
4. Add texture paths in the inspector. Type any entry name or reuse one from the dropdown.
5. Adjust the shared mapping and choose which texture entry to preview.
6. Open **Export**, select the outputs you need, and choose their suffixes and formats.
7. Import the exported files into your texturing tool or game engine.

BaseColor, Normal and ORM are examples, not fixed slots. Custom names work the same way. Texture files remain linked externally; keep them beside the project and use relative paths when moving projects between computers.

## Export formats

| Format | Use |
| --- | --- |
| **PNG** | Texture sheets at 8 or 16 bits per channel; ID textures, masks and raster guides at 8 bits |
| **TGA** | Texture sheets, ID textures, masks and guides with 8-bit RGBA channels |
| **SVG** | Vector layout guides |
| **JSON** | Pixel rectangles, UV coordinates, labels and texture metadata for scripts |
| **CSV** | Region measurements for spreadsheets and pipeline tools |

Export choices start unchecked. Each texture output has its own suffix and format, with optional edge dilation.

For normal maps, **Invert green channel (normal Y)** changes the Y convention without modifying the source image. Channel packing and material baking remain in your texturing software. Set the appropriate color or data interpretation when importing textures into an engine.

## Updates and switching editions

Use **Help > Updates** to check for a compatible published update, download it and restart. A trusted update ZIP can also be imported manually. Updates preserve `Data/` and retain the bundled build as a fallback. Update assets must be published for the matching edition and operating system; portable download ZIPs alone do not enable the updater.

Main and Mini use separate desktop hosts and update formats. They do not automatically switch editions. To switch, extract the other edition into a new folder and reopen your projects. Do not merge their runtime folders, browser caches or active-update files. See `Help/docs/UPDATES.md` inside the download for settings migration instructions.

During 0.1 alpha, build numbers identify newer releases.

## Documentation and source

Portable downloads include the user guide, texture workflow, project/export schema documentation and platform notes under `Help/docs/`. Required third-party notices are consolidated in `Help/THIRD-PARTY-NOTICES.md`.

The editor is written in React and TypeScript, with layout math and export logic separated from the desktop host. The main edition uses Electron; Mini uses Tauri and Rust for native functions. Development prerequisites differ, so follow `docs/BUILD.md` in the corresponding source package.

For the main edition, with Node.js 24.19.0 installed:

```sh
npm ci
npm test
npm run test:desktop
npm run build
npm run desktop
```

Source packages include build scripts, automated tests, schemas and sample projects. Downloadable application ZIPs are distributed as GitHub Release assets.

## Feedback

This is an alpha release. When reporting a problem, include the edition (main or Mini), operating system, build number, reproduction steps and a small sample project. Only attach textures you have permission to share.

Windows packages are unsigned and may trigger SmartScreen warnings. Native desktop acceptance testing remains incomplete; automated layout and file-operation checks do not cover every machine or graphics driver.

## License and credits

See [LICENSE](LICENSE) for the application's license. Third-party components retain their own terms; their notices are included with each download.

The zone-and-strip workflow was inspired by [Trim Sheet Architect](https://github.com/btitkin/TrimSheetArchitect). TurboTrimmer's implementation is independent.
