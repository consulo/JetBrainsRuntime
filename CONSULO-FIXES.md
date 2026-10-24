# Consulo changes to JetBrains Runtime

This fork is JetBrains Runtime 25 with changes needed by Consulo. Upstream JetBrains
changes are merged in as usual.

## Linux - LoongArch64

Upstream JBR 25 runs on LoongArch64 only in interpreter mode (Zero). This fork adds
the full HotSpot port with the JIT compilers (C1 and C2).

## Linux - Wayland tooltips

Fixes for Swing tooltips under the native Wayland toolkit, for any look and feel,
including FlatLaf:

- A tooltip no longer appears under the mouse pointer. When there is no space below
  the pointer (for example on the bottom tool window stripe), it is shown above it.
- Tooltips keep their normal delays instead of appearing instantly after the first
  one, and moving along a long button no longer produces a "train" of tooltips.

Related JetBrains issue: [JBR-6391](https://youtrack.jetbrains.com/issue/JBR-6391)
"Wayland: tooltips flicker when appear over the mouse pointer". JetBrains fixed only
the flicker; the tooltip still appeared under the pointer, and that fix caused the
missing delays.

## Haiku

The Haiku port is part of this repository, so there is no separate JDK repository for
Haiku anymore.

- Builds natively on Haiku (there is no cross toolchain). The boot JDK is OpenJDK 24
  from Haiku packages, and ASLR has to be disabled while building and running.
- Uses its own AWT toolkit with Haiku windows, the same as before the merge.
- JetBrains-only features that need Linux, Wayland, X11 or Vulkan are turned off on
  Haiku.
- UI scale is detected from the system font size: 12pt means scale 1.0, bigger fonts
  give a proportionally bigger scale (fractional values are supported).
- Crash logs show "not available on this platform" for process memory usage.
