# shrink

Resize images in a directory so they fit within a maximum width and height.
Aspect ratio is always preserved. Files already within the limits are left
untouched.

## Install

```sh
go install github.com/lxkrmr/shrink@latest
```

Requires Go. The binary lands in `~/go/bin/shrink`, which should already be
in your `$PATH` if you have used `go install` before.

## Usage

```sh
shrink --max-width N --max-height N <dir>
```

At least one of `--max-width` or `--max-height` is required. Flags must come before the directory.

```sh
# resize everything in ~/Screenshots to fit within 1280×1280
shrink --max-width 1280 --max-height 1280 ~/Screenshots

# current directory, only constrain width
shrink --max-width 1920 .
```

Shell alias example:

```sh
alias shrink='shrink --max-width 1280 --max-height 1280 ~/Screenshots'
```

## Output

```
screenshot-big.png: 3200×2400 → 1280×960 (4.2 MB → 0.9 MB)
screenshot-ok.png: ok (1024×768)

2 resized, 1 ok, 0 failed
```

Errors go to stderr. Exit code is `0` if all files were processed, `1` if any
file failed.

## Supported formats

PNG, JPEG. Files with other extensions are silently skipped.

## Flags

| Flag | Description |
|---|---|
| `--max-width N` | Maximum width in pixels |
| `--max-height N` | Maximum height in pixels |
| `--version` | Print version and exit |
