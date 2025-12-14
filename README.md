# nvr-go

A lightweight Go implementation of [neovim-remote](https://github.com/mhinz/neovim-remote), specifically written for the [neomux](https://github.com/nikvdp/neomux) plugin.

## What is this?

This is a Go replacement for the Python `nvr` tool. It doesn't implement all features of the original neovim-remote - just the subset needed by neomux for remote-controlling Neovim instances from shell scripts and terminal buffers.

**Why Go instead of Python?**
- Single static binary - no Python runtime or pip dependencies
- Faster startup time
- Easier distribution across platforms

## Installation

### From releases

Download the appropriate binary from the [releases page](https://github.com/nikvdp/nvr-go/releases).

### From source

```bash
go install github.com/nikvdp/nvr-go@latest
```

Or clone and build:

```bash
git clone https://github.com/nikvdp/nvr-go.git
cd nvr-go
go build -o nvr .
```

## Usage

```bash
# Open files in existing Neovim instance
nvr file1.txt file2.txt
nvr --remote file.txt

# Open file and wait until buffer is closed (useful for git commit messages)
nvr --remote-wait file.txt

# Open file in new tab
nvr --remote-tab file.txt

# Open file in horizontal split
nvr -o file.txt

# Open file in vertical split  
nvr -O file.txt

# Execute Neovim command
nvr -c "echo 'hello'"

# Execute command before opening files
nvr -cc split file.txt

# Evaluate expression and print result
nvr --remote-expr "getcwd()"

# Read from stdin
echo "content" | nvr -

# Test connection to Neovim
nvr --test
```

## Socket Discovery

nvr-go finds your Neovim instance by checking (in order):

1. `$NVIM` environment variable (set automatically by Neovim's terminal)
2. `$NVIM_LISTEN_ADDRESS` environment variable

## Implemented Features

- `--remote` - Open files with `:edit`
- `--remote-wait` - Open files and wait for buffer close
- `--remote-tab` - Open files with `:tabedit`
- `--remote-expr` - Evaluate Vimscript expression
- `-c` - Execute command after opening files
- `-cc` - Execute command before opening files
- `-o` - Use horizontal split
- `-O` - Use vertical split
- `-` - Read from stdin

## Not Implemented

These features from the original nvr are **not** implemented:

- `--remote-send` - Send keys
- `--servername` - Specify server name
- `--nostart` - Don't start new instance
- `-l` / `-p` / `-t` flags
- Starting a new Neovim instance if none exists

If you need these features, use the original [neovim-remote](https://github.com/mhinz/neovim-remote).

## Requirements

- Neovim 0.5+
- Unix-like OS (Linux, macOS, BSD)

## License

MIT
