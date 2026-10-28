# Modifications in this fork

This repository, https://github.com/kuanyui/lha, is a fork of LHa for UNIX
(https://github.com/jca02266/lha). It builds `lha.exe` for Windows (x86_64), and `lha` for
macOS (Apple silicon and Intel).

Its changes to LHa for UNIX:

- `src/lha_macro.h`: when built with MinGW-w64 without the MSYS2 compatibility layer
  (`__MINGW32__` without `__MSYS__`), symbolic links are not supported: `symlink()` always
  fails, `lstat` is `stat`, and `S_ISLNK()` is always false.
- `configure.ac`: the version gets the suffix `-kyYYYYMMDD`, where `YYYYMMDD` is the date
  of a release of this fork. For example, `1.14i-ac20260723-ky20261014` is the release of
  2026-10-14, based on `1.14i-ac20260723`. This suffix identifies this fork in the output
  of `lha --version` and in the names of the ZIP files.
- `.github/workflows/build.yaml`: builds `lha.exe` and `lha`. The workflow packs each of
  them with this file (`FORK_MODIFICATIONS.md`) and `lha-VERSION-src.zip`.
  `lha-VERSION-src.zip` is the source code of the commit that both binaries were built from.
  For a tag whose name is the version in `configure.ac`, the workflow also puts both
  packages on the release page of the tag.
  - `lha-VERSION-win64.zip` has `lha.exe`. It is built with MSYS2 (MINGW64), and statically
    linked with libiconv.
  - `lha-VERSION-macos-universal.zip` has `lha`. It is a universal binary for Apple silicon
    (arm64) and Intel (x86_64). It runs on macOS 12 or later, and uses the libiconv of
    macOS. It converts file names to "UTF-8", not to "UTF-8-MAC". UTF-8-MAC writes some
    characters as several code points: for example, が as か and a combining ゛.
- This file.

## The packages of `lha.exe` and `lha`

The terms of redistribution of LHa for UNIX (`man/lha.man`, in Japanese) do not allow
distributing the binary alone. So `lha.exe` and `lha` always come with:

- this file;
- `lha-VERSION-src.zip`: the source code of the commit that the binary was built from,
  including the documents of LHa for UNIX.
