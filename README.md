# Ports Dashboard for macOS (`ports.py`)

A small terminal dashboard that shows which app or Docker container is using TCP ports on your Mac. Optimized for development ports **3000–9999**. Uses `lsof` for host processes and `docker ps` for container mappings.

## Features

* Live, scroll-free view of ports in a range
* **Unique Ports mode** (default) that shows one line per port
* **Detail mode** that shows process, PID, user, local and remote
* Docker integration: maps host port → container name, image, and container port
* Keyboard controls to toggle modes and refresh rate
* Safe rendering on small terminals

## Requirements

* macOS
* Python 3.8+
* `lsof` (`brew install lsof`)
* Docker Desktop (optional, for container mapping)
* `sudo` is recommended so `lsof` can see all processes

## Quick start

```bash
# Make it executable
chmod +x /Users/adar.bahar/code/python/ports/ports.py

# Run directly
sudo /Users/adar.bahar/code/python/ports/ports.py
```

## Install: run from any path (recommended symlink on PATH)

The cleanest way is to symlink the script into a folder on your PATH. Example using `~/bin`.

```bash
# 1) Ensure the script is executable
chmod +x /Users/adar.bahar/code/python/ports/ports.py

# 2) Create a personal bin directory if you do not have one
mkdir -p "$HOME/bin"

# 3) Symlink with a short name
ln -sf /Users/adar.bahar/code/python/ports/ports.py "$HOME/bin/ports"

# 4) Add ~/bin to PATH if needed (zsh)
if ! echo "$PATH" | grep -q "$HOME/bin"; then
  echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc
  source ~/.zshrc
fi

# 5) Verify
which ports
ports -h 2>/dev/null || true
```

Now you can run:

```bash
ports            # or: sudo ports
```

### Alternative: symlink into /usr/local/bin

```bash
sudo ln -sf /Users/adar.bahar/code/python/ports/ports.py /usr/local/bin/ports
```

### Optional wrapper to always run with sudo

```bash
printf '%s\n' '#!/bin/sh' 'exec sudo "$HOME/bin/ports" "$@"' | tee "$HOME/bin/ports-sudo" >/dev/null
chmod +x "$HOME/bin/ports-sudo"
# Run: ports-sudo
```

## Usage

Run in a terminal at least 80×24 for comfort.

```bash
ports          # normal
sudo ports     # full visibility
```

### Keys

* `u` toggle Unique Ports or Detail
* `l` toggle only LISTEN
* `d` toggle showing Docker-only published ports
* `+` and `-` change refresh rate
* `q` quit

### What you will see

* **Unique mode**: Port, state, a short list of processes, containers, and images, plus hints about local address and container ports
* **Detail mode**: One row per PID or container mapping with `LOCAL → REMOTE` and container port annotations

## Configuration

Edit the constants at the top of `ports.py`:

```python
LO_PORT = 3000
HI_PORT = 9999
REFRESH_SECS_DEFAULT = 2.0
```

## Docker notes

* Docker Desktop publishes container ports via a host proxy. The dashboard reads `docker ps` to map host ports to containers and adds rows labeled `PUBLISHED` when relevant.
* If Docker is not installed or not running, Docker features are skipped automatically.

## Troubleshooting

* **`Error: lsof not found`**: `brew install lsof`
* **No results**: Ensure there are listeners in 3000–9999. Press `l` to toggle only LISTEN. Try widening the port range in the script.
* **`_curses.error: addnwstr() returned ERR`**: Make the terminal window larger or reduce font size.
* **Docker rows missing**: Ensure Docker Desktop is running and containers expose ports in the configured range. Try `docker ps` to confirm.

## Security

* `sudo` gives the script permission to read other users' sockets via `lsof`. Review the source if you have concerns.
* The script only runs `lsof` and `docker ps` and prints parsed results. It does not open ports or modify processes.

## Uninstall

Remove the symlink and PATH line you added.

```bash
rm -f "$HOME/bin/ports"
# Optionally remove PATH edit from ~/.zshrc if you added it
```

## License

Use freely for personal or work projects. Add a license file if you plan to redistribute.
