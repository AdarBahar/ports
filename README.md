# 🚀 Ports Manager

A terminal-based tool for monitoring network ports and processes on macOS and Linux. Built for developers working with multiple services, containers, and microservices.

![Ports Manager Demo](https://img.shields.io/badge/Platform-macOS%20%7C%20Linux-blue)
![Python Version](https://img.shields.io/badge/Python-3.8%2B-green)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Version](https://img.shields.io/badge/Version-2.1.2-brightgreen)

## ✨ Features

### � **Port Monitoring**
* **Real-time TCP port monitoring** with configurable ranges (default: 3000-9999)
* **Dual display modes**: Unique (aggregated) and Detail (per-process) views
* **Filtering options**: LISTEN-only mode, Docker integration
* **Process correlation**: Links ports to running processes with full details

### 🔄 **Automatic Updates**
* **GitHub integration** for automatic version checking and updates
* **Safe update process** with backup and rollback protection
* **One-click updates** with automatic restart

### 🐳 **Docker Integration**
* **Container detection** and port mapping correlation
* **Container metadata**: names, images, internal port mappings
* **Docker-published port visibility** for containerized services

### 🏷️ **Alias System**
* **Per-entry aliases**: Custom names for specific port/process combinations
* **Per-process aliases**: Global friendly names for process types
* **Built-in friendly names** for common services (nginx, MySQL, Redis, etc.)
* **Persistent storage** with automatic backup

## 📋 System Requirements

### Runtime Dependencies
* **Python 3.8+** (standard library only)
* **lsof** command-line tool
* **macOS** (10.14+) or **Linux** (Ubuntu 18.04+, CentOS 7+)

### Install System Dependencies
```bash
# macOS
brew install lsof

# Ubuntu/Debian
sudo apt update && sudo apt install lsof

# CentOS/RHEL/Fedora
sudo yum install lsof  # or: sudo dnf install lsof
```

### Optional
* **Docker** (for container port mapping)
* **sudo access** (for full process visibility)

## 🚀 Installation

### Quick Install
```bash
# Clone and install
git clone https://github.com/AdarBahar/ports.git
cd ports
chmod +x ports

# System-wide (recommended)
sudo cp ports /usr/local/bin/

# Or user-only
mkdir -p "$HOME/bin" && cp ports "$HOME/bin/"
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc  # Add to PATH if needed
```

## 📖 Usage

### Basic Commands
```bash
# Run with current user permissions
ports

# Run with elevated permissions (recommended for full visibility)
sudo ports

# Command line options
ports --version    # Show version
ports --help       # Show help
ports --no-update  # Skip update check
```

### Keyboard Controls

| Key | Action | Description |
|-----|--------|-------------|
| `q` | Quit | Exit the application |
| `u` | Toggle Mode | Switch between Unique and Detail views |
| `l` | LISTEN Filter | Show only listening sockets |
| `d` | Docker Toggle | Include/exclude Docker-published ports |
| `+` / `-` | Refresh Rate | Increase/decrease update frequency |
| `a` | Add Alias | Create custom alias for selected row |
| `x` | Delete Alias | Remove alias from selected row |
| `g` | Process Alias | Set global alias for process type |
| `?` | Help | Show help screen |
| `ESC` | Cancel | Cancel current operation |

### Display Modes

**Unique Mode** (Default): One line per port with aggregated information
**Detail Mode**: One line per process/container with full details

## ⚙️ Configuration

### Port Range
Edit the `ports` script to change monitoring range:
```python
DEFAULT_PORT_RANGES = [(3000, 9999)]  # Default range
```

### Aliases
- **Per-entry**: Press `a` to alias specific port/process combinations
- **Per-process**: Press `g` to alias all instances of a process type
- **Built-in names**: Automatic friendly names for common services (nginx, MySQL, Redis, etc.)
- **Storage**: Saved to `~/.ports_aliases.json`

### Updates
- **Automatic checking**: Checks GitHub for updates on startup
- **Safe updates**: Press `u` when prompted to update with automatic backup
- **Skip updates**: Use `--no-update` flag to skip version checking

## 🔧 Development

### Development Dependencies
The project includes a `requirements.txt` file with optional development tools:
```bash
# Install development dependencies (optional)
pip install -r requirements.txt
```

**Note**: The application itself requires **zero external dependencies** and runs with Python's standard library only.

### Development Tools (Optional)
- `black` - Code formatting
- `flake8` - Code linting
- `mypy` - Type checking
- `pytest` - Testing framework

## 🔧 Troubleshooting

| Issue | Solution |
|-------|----------|
| `Error: lsof not found` | Install lsof: `brew install lsof` (macOS) or `sudo apt install lsof` (Linux) |
| No ports shown | Check port range, press `l` to toggle LISTEN filter, try `sudo` for full visibility |
| Docker containers missing | Ensure Docker is running: `docker ps` |
| Permission denied | Run with `sudo` for full process visibility |
| Slow performance | Reduce refresh rate with `-` key |

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

**Made with ❤️ for developers who juggle multiple services and containers**
