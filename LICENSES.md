# Licences of everything compiled into libmpv-2.dll

The DLL as a whole is offered under the **GNU LGPL, version 2.1 or later**:
mpv is built with `-Dgpl=false` and FFmpeg without `--enable-gpl`,
`--enable-version3` or `--enable-nonfree` (see `patches/lgpl.patch`). The CI
"GPL guard" step checks the built configuration and the DLL itself.

The libraries below are linked statically. Each keeps its own licence; the
source archive attached to every release holds their full source and licence
files. Versions are whatever the pinned recipes (`pins.env`) fetched; the
source archive records the exact trees.

| Library | Role | Licence |
|---|---|---|
| mpv (`-Dgpl=false`) | player core, libmpv API | LGPL-2.1-or-later |
| FFmpeg (no gpl/version3/nonfree) | demux, decode, scale, PNG/JPEG encode | LGPL-2.1-or-later |
| libplacebo | GPU rendering | LGPL-2.1-or-later |
| fribidi | bidirectional text | LGPL-2.1-or-later |
| libiconv (GNU) | charset conversion | LGPL-2.1-or-later (library) |
| uchardet | charset detection | tri-licence MPL-1.1 / GPL-2.0+ / LGPL-2.1+; used under **LGPL-2.1+ or MPL-1.1** |
| subrandr (+ its Rust crates, Rust std) | SRV3/WebVTT subtitles | MPL-2.0 (crates: see open question below) |
| libass | ASS subtitles | ISC |
| freetype2 | font rendering | dual FTL / GPL-2.0; used under **FTL** (credit line required) |
| harfbuzz | text shaping | MIT ("Old MIT") |
| fontconfig | font lookup | MIT-style (HPND) |
| libunibreak | line breaking | Zlib |
| libxml2 | XML (fontconfig, FFmpeg) | MIT |
| dav1d | AV1 decoding | BSD-2-Clause |
| libzimg, graphengine | scaling (zimg) | WTFPL |
| lcms2 | colour management | MIT |
| libjpeg-turbo | JPEG screenshots | IJG + BSD-3-Clause + Zlib |
| libpng | PNG | libpng-2.0 |
| zlib-ng | compression | Zlib |
| bzip2 | compression (FFmpeg) | bzip2-1.0.6 (BSD-style) |
| xxhash | hashing | BSD-2-Clause |
| luajit | Lua scripting | MIT |
| mujs | JavaScript scripting | ISC |
| shaderc, glslang | shader compiler | Apache-2.0 (glslang also BSD-3-Clause and others) |
| SPIRV-Tools | shader tools | Apache-2.0 |
| SPIRV-Cross | shader translation (D3D11) | Apache-2.0 |
| SPIRV-Headers | headers | MIT (Khronos) |
| Vulkan-Loader | Vulkan | Apache-2.0 |
| Vulkan-Headers | headers | Apache-2.0 OR MIT |
| glad | OpenGL loader (generated) | MIT generator; generated code CC0 / Apache-2.0 |
| fast_float | number parsing (headers) | Apache-2.0 OR MIT OR BSL-1.0 |
| ANGLE headers | EGL/GLES headers | BSD-3-Clause |
| nv-codec-headers | NVDEC/NVENC headers | MIT |
| mingw-w64 CRT, winpthreads | C runtime | ZPL-2.1 / public domain; MIT-style |
| libc++, libunwind (clang build) | C++ runtime | Apache-2.0 WITH LLVM-exception |
| libstdc++, libgcc (gcc build) | C++ runtime | GPL-3.0 WITH GCC-exception-3.1 |

**Removed from the upstream recipes** because HighlightFab does not need them:
libarchive (and with it **lzo, GPL-2.0+**, and xz), libzvbi, libaribcaption,
libbs2b.

## Open points for legal review

- **Apache-2.0 + LGPL-2.1+.** The FSF regards Apache-2.0 as incompatible with
  (L)GPL **version 2** but compatible with version 3. mpv and FFmpeg are
  "2.1 or later", so the combined DLL may effectively have to be distributed
  under **LGPL-3.0** terms. That is still LGPL (dynamic linking and
  replacement allowed), but LGPL-3.0 adds the "installation information" rule.
- **subrandr's Rust dependencies** need their own licence list (e.g. with
  `cargo about`); disabling subrandr (`-Dsubrandr=disabled`) removes the
  question if HighlightFab does not need SRV3/WebVTT rendering.
- **FreeType (FTL)** requires a credit in the product documentation.
