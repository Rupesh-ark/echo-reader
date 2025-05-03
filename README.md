# Reader App

A cross-platform, scalable reader application written in Zig. It supports HTML, EPUB, and PDF formats, offers customizable fonts and themes, and — uniquely — analyzes the mood of your text on-the-fly to select and play a matching soundtrack.

## Features

* **Multi-format support**: Load and read HTML, EPUB, and PDF files seamlessly.
* **Customizable experience**: Adjust fonts, themes, and layouts for comfortable reading.
* **Mood-based soundtrack**: Real-time text analysis (sentiment/mood) drives a dynamic music playlist.
* **Clean architecture**: Decoupled layers (Core → Infrastructure → Services → UI) for easy testing, extension, and maintenance.
* **Cross-platform**: Builds and runs on Linux, Windows, and macOS.

## Architecture Overview

```
┌─────────────────────────────────────────┐
│                UI Layer                │   ← GTK/WebKit or SDL/NanoVG
│  • User interactions, rendering, menus │
└─────────────────────────────────────────┘
                  ▲
                  │
┌─────────────────────────────────────────┐
│          Application (Services)        │   ← Orchestrates use-cases
│  • Open file, analyze mood, play music │
└─────────────────────────────────────────┘
                  ▲
                  │
┌─────────────────────────────────────────┐
│              Domain/Core               │   ← Pure Zig logic
│  • File parsers, sentiment analyzer    │
│  • Mood-to-playlist mapper             │
└─────────────────────────────────────────┘
                  ▲
                  │
┌─────────────────────────────────────────┐
│          Infrastructure Layer          │   ← C libraries, OS, network
│  • Unzip (miniz), XML (libxml2), PDF   │
│    renderer (Poppler), audio (GStreamer) │
└─────────────────────────────────────────┘
```

## Getting Started

### Prerequisites

* [Zig](https://ziglang.org/) (version 0.11.0 or later)
* Development headers for GTK4, WebKit2GTK, Poppler-GLib, and GStreamer
* C compiler (GCC/Clang on Linux/macOS, MSVC or MinGW on Windows)

### Building

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/reader-app.git
   cd reader-app
   ```
2. Build the project:

   ```bash
   zig build
   ```
3. Run tests:

   ```bash
   zig test
   ```
4. Launch the application:

   ```bash
   ./zig-out/bin/reader-app
   ```

## Usage

1. Open a file via **File → Open** or drag-and-drop an HTML, EPUB, or PDF onto the window.
2. Customize fonts, theme, and layout in **Settings**.
3. As you read, the app analyzes the text and transitions the background music to match the mood.

## Project Layout

```
reader-app/
├── build.zig            # Build script
├── src/
│   ├── core/            # Pure Zig domain logic
│   ├── infra/           # C bindings & OS integration
│   ├── app/             # Application services/use-cases
│   └── ui/              # UI bindings & entry point
├── tests/               # Unit & integration tests
├── assets/              # CSS themes, fonts, sample playlists
└── zig-cache/           # Built artifacts (ignored)
```

## License

[MIT License](LICENSE)

---

Built with ❤️ in Zig. Feel free to reach out with feedback or questions!
