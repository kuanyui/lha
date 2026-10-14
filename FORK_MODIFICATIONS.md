# Modifications in this fork

This repository, https://github.com/kuanyui/lha, is a fork of LHa for UNIX
(https://github.com/jca02266/lha). It builds `lha.exe` for Windows (x86_64).

Its changes to LHa for UNIX:

- `src/lha_macro.h`: when built with MinGW-w64 without the MSYS2 compatibility layer
  (`__MINGW32__` without `__MSYS__`), symbolic links are not supported: `symlink()` always
  fails, `lstat` is `stat`, and `S_ISLNK()` is always false.
- `configure.ac`: the version gets the suffix `-kyYYYYMMDD`, where `YYYYMMDD` is the date
  of a release of this fork. For example, `1.14i-ac20260723-ky20261014` is the release of
  2026-10-14, based on `1.14i-ac20260723`. This suffix identifies this fork in the output
  of `lha --version` and in the names of both ZIP files.
- `.github/workflows/build-windows.yaml`: builds `lha.exe` with MSYS2 (MINGW64), statically
  linked with libiconv. The workflow packs `lha.exe`, this file (`FORK_MODIFICATIONS.md`),
  and `lha-VERSION-src.zip` into `lha-VERSION-win64.zip`. `lha-VERSION-src.zip` is the
  source code of the commit that `lha.exe` was built from. For a tag whose name is the
  version in `configure.ac`, the workflow also puts `lha-VERSION-win64.zip` on the release
  page of the tag.
- This file.

## The package of `lha.exe`

The terms of redistribution of LHa for UNIX (`man/lha.man`, in Japanese) do not allow
distributing the binary alone. So `lha.exe` always comes with:

- this file;
- `lha-VERSION-src.zip`: the source code of the commit that `lha.exe` was built from,
  including the documents of LHa for UNIX.
