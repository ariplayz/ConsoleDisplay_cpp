<div align="center">

# 🖥️ ConsoleDisplay

### *A Modern C++ Library for Console Graphics*

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![C++](https://img.shields.io/badge/C++-20-orange.svg)
![License](https://img.shields.io/badge/license-GPL--3.0-green.svg)

**Transform your terminal into a 512×512 pixel canvas**

[Features](#-features) • [Quick Start](#-quick-start) • [API](#-api-reference) • [Examples](#-examples)

</div>

---

## ✨ Features

- 🎨 **Dual-Mode Rendering** — Each cell can be a pixel or text character
- 📐 **Large Canvas** — 512×512 grid for detailed visualizations
- 🚀 **Zero Dependencies** — Pure C++ with STL only
- 🎯 **Bounds-Safe** — Automatic handling of out-of-bounds operations
- 🧪 **Test-Friendly** — Perfect for unit testing ASCII output
- ⚡ **Lightweight** — Simple and efficient design

## 🚀 Quick Start

```cpp
#include <ConsoleDisplay/library.h>
#include <iostream>

int main() {
    console_display::ConsoleDisplay display;

    // Draw some pixels
    display.setPixel(10, 10, true);
    display.setPixel(11, 10, true);
    display.setPixel(12, 10, true);

    // Add text
    display.setTextString(0, 0, "Hello, Console!");

    // Render to terminal
    display.render(std::cout);
}
```

## 📦 Installation

Include the header in your project:

```cpp
#include <ConsoleDisplay/library.h>
```

Link against the ConsoleDisplay library in your build system.

## 📚 API Reference

### Core Class

```cpp
namespace console_display {
    class ConsoleDisplay {
        static constexpr int WIDTH = 512;
        static constexpr int HEIGHT = 512;
        // ...
    };
}
```

### 🎯 Cell Types

```cpp
enum class CellType : std::uint8_t {
    Empty,  // Uninitialized cell
    Pixel,  // Binary on/off pixel
    Text    // Character cell
};

struct Cell {
    CellType type;
    bool     pixelOn;
    char     ch;
};
```

### 🛠️ Methods

#### Construction & Clearing

| Method | Description |
|--------|-------------|
| `ConsoleDisplay()` | Creates a new display with all cells cleared |
| `void clear()` | Resets all cells to empty state |

#### Pixel Operations

| Method | Description |
|--------|-------------|
| `void setPixel(int x, int y, bool on = true)` | Set a pixel on/off at coordinates |
| `void fillPixels(bool on)` | Fill entire grid with pixels |

#### Text Operations

| Method | Description |
|--------|-------------|
| `void setText(int x, int y, char ch)` | Place a character at coordinates |
| `void setTextString(int x, int y, const std::string& s)` | Write a horizontal string |

#### Rendering & Access

| Method | Description |
|--------|-------------|
| `Cell getCell(int x, int y) const` | Retrieve cell at coordinates |
| `std::string toString(char pixelChar = '#', char emptyChar = ' ') const` | Convert grid to string |
| `void render(std::ostream& os) const` | Output to stream |

## 💡 Examples

### Drawing a Box

```cpp
console_display::ConsoleDisplay display;

// Draw horizontal lines
for (int x = 0; x < 20; ++x) {
    display.setPixel(x, 0, true);
    display.setPixel(x, 10, true);
}

// Draw vertical lines
for (int y = 0; y < 11; ++y) {
    display.setPixel(0, y, true);
    display.setPixel(19, y, true);
}

display.render(std::cout);
```

### Custom Pixel Characters

```cpp
console_display::ConsoleDisplay display;
display.fillPixels(true);

// Render with custom characters
std::string output = display.toString('█', '░');
std::cout << output;
```

### Text Banner

```cpp
console_display::ConsoleDisplay display;
display.setTextString(5, 5, "╔════════════╗");
display.setTextString(5, 6, "║  Welcome!  ║");
display.setTextString(5, 7, "╚════════════╝");
display.render(std::cout);
```

## 📝 Notes

- **Coordinate System**: Origin (0,0) is at top-left
- **Bounds Handling**: Out-of-bounds operations are silently ignored
- **Thread Safety**: Not thread-safe; use external synchronization if needed
- **Performance**: O(1) for pixel/text operations, O(WIDTH × HEIGHT) for rendering

## 🏗️ Building

The library uses Meson build system. See `meson.build` for configuration.

## 📄 License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details.

### GPL-3.0 Summary

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

## 👨‍💻 Authors

**JetBrains Autonomous Programmer (Junie)**

---

<div align="center">

**[⬆ Back to Top](#-consoledisplay)**

Made with ❤️ for the console graphics community

</div>
