# Software Investigator

A command-line tool that inspects executable files and reports their structure, **without ever running them**.
Written in C, no third-party libraries. Currently supports ELF files on Linux.

> **Status:** early release (v0.1.0). Educational parser, actively developed.

## What it does

Point it at a file and it tells you what the file is and how it is laid out:

1. **File summary:** size and detected format (ELF, PE, or unknown).
2. **ELF basics:** architecture (32/64-bit), byte order, file type, target machine, entry point.
3. **Program segments:** how the loader maps the file into memory.
4. **Sections:** the logical parts of the file (code, data, symbol tables, and so on).
5. **Symbols:** entries from `.dynsym` and `.symtab`, up to 40 per table.
6. **Raw byte preview:** the first bytes of the file.

Safety design: every table offset, size, and string reference is range-checked before it is read, so a damaged or
hostile file produces an error message instead of a crash. A stripped binary with no symbol tables is reported
normally, not treated as a failure.

## Download and run

1. Go to the **Releases** page of this repository and download the binary for your platform.
2. Make it executable and run it:

```sh
chmod +x investigator
./investigator inspect /bin/ls
./investigator inspect ./some-file
./investigator --help
```

Platforms: **Linux x86_64** only for now.

## Example output

```
(paste a real run of ./investigator inspect <file> here)
```

## Limitations

- Linux and ELF only. PE files are recognised by format detection, but their contents are **not parsed yet**.
- Not a complete ELF implementation: extended ELF numbering and relocations are not handled yet, and symbol
  handling is partial.
- Output is bounded (for example, 40 symbols per table) to stay readable.
- This tool is for analysis and learning. It makes no guarantee that its results are complete or correct, so do
  not rely on it alone for security decisions.

## Roadmap

- PE header, section, and import parsing
- Relocations and fuller symbol semantics
- Windows binary release

## License

This software is **proprietary**. You may run it for personal, educational, or evaluation use. Redistribution,
modification, and reverse engineering are not permitted. See [LICENSE](LICENSE) for the full terms.

## Author

Mohit Sheoran, Ghaziabad, India. GitHub: [imohitsheoran.github.io](https://imohitsheoran.github.io)
