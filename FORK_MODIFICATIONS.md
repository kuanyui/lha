# Modifications in this fork

This repository, https://github.com/kuanyui/lha, is a fork of LHa for UNIX
(https://github.com/jca02266/lha). It builds `lha.exe` for Windows (x86_64).

Its changes to LHa for UNIX:

- `src/lha_macro.h`: when built with MinGW-w64 without the MSYS2 compatibility layer
  (`__MINGW32__` without `__MSYS__`), symbolic links are not supported: `symlink()` always
  fails, `lstat` is `stat`, and `S_ISLNK()` is always false.
- `.github/workflows/build-windows.yaml`: builds `lha.exe` with MSYS2 (MINGW64), statically
  linked with libiconv, and packs it with this file and its source code.
- This file.

## The package of `lha.exe`

The terms of redistribution of LHa for UNIX (`man/lha.man`, in Japanese) do not allow
distributing the binary alone. So `lha.exe` always comes with:

- this file;
- `lha-VERSION-src.zip`: the source code of the commit that `lha.exe` was built from,
  including the documents of LHa for UNIX.
