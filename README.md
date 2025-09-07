# 🚀 Ports Manager

A powerful, optimized terminal-based tool for monitoring network ports and processes on macOS and Linux. Perfect for developers working with multiple services, containers, and microservices.

![Ports Manager Demo](https://img.shields.io/badge/Platform-macOS%20%7C%20Linux-blue)
![Python Version](https://img.shields.io/badge/Python-3.8%2B-green)
![License](https://img.shields.io/badge/License-MIT-yellow)
![SPDX License](https://img.shields.io/badge/SPDX--License--Identifier-MIT-blue)

## ✨ Features

### 🔍 **Smart Port Monitoring**
* **Live, real-time view** of TCP ports in configurable range (default: 3000-9999)
* **Dual display modes**: Unique (aggregated) and Detail (per-process) views
* **Intelligent filtering**: LISTEN-only mode, Docker integration
* **Zero-scroll interface** with automatic terminal size adaptation

### 🐳 **Docker Integration**
* **Automatic container detection** and port mapping
* **Container metadata display**: names, images, internal ports
* **Docker-only port visibility** for published container ports
* **Seamless host-container correlation**

### 🎨 **Advanced UI/UX**
* **Color-coded connection states** (LISTEN, ESTABLISHED, PUBLISHED)
* **Responsive layout** that adapts to terminal size
* **Comprehensive help system** with ESC key support
* **Intuitive keyboard shortcuts** for all operations

### 🏷️ **Powerful Alias System**
* **Per-entry aliases**: Custom names for specific port/process combinations
* **Per-process aliases**: Global friendly names for process types
* **Built-in friendly names** for common services (nginx, MySQL, Redis, etc.)
* **Persistent storage** with automatic backup and recovery

### ⚡ **Performance Optimized**
* **Compiled regex patterns** for maximum parsing speed
* **Efficient data structures** with proper typing
* **Minimal memory footprint** and CPU usage
* **Robust error handling** with graceful degradation

## 📋 Requirements

### System Requirements
* **macOS** (10.14+) or **Linux** (Ubuntu 18.04+, CentOS 7+)
* **Python 3.8+** with standard library
* **lsof** command-line tool

### Installation Commands
```bash
# macOS (Homebrew)
brew install lsof

# Ubuntu/Debian
sudo apt update && sudo apt install lsof

# CentOS/RHEL/Fedora
sudo yum install lsof  # or: sudo dnf install lsof
```

### Optional Dependencies
* **Docker** (for container port mapping)
* **sudo access** (recommended for full process visibility)

## 🚀 Quick Start

### Method 1: Direct Execution
```bash
# Clone the repository
git clone https://github.com/AdarBahar/ports.git
cd ports

# Make executable and run
chmod +x ports
sudo ./ports
```

### Method 2: System-wide Installation (Recommended)

```bash
# Clone and install
git clone https://github.com/AdarBahar/ports.git
cd ports

# Make executable
chmod +x ports

# Install to system PATH
sudo cp ports /usr/local/bin/

# Verify installation
which ports
ports --help 2>/dev/null || echo "Ready to run with: sudo ports"
```

### Method 3: User Installation

```bash
# Clone the repository
git clone https://github.com/AdarBahar/ports.git
cd ports

# Make executable
chmod +x ports

# Create personal bin directory
mkdir -p "$HOME/bin"

# Install to user PATH
cp ports "$HOME/bin/"

# Add to PATH (if not already)
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc  # or ~/.zshrc
source ~/.bashrc  # or source ~/.zshrc

# Verify
which ports
```

### Running the Application

```bash
# Basic usage
ports

# With full process visibility (recommended)
sudo ports

# Check dependencies
ports --help
```

## 📖 Usage Guide

### Basic Usage
```bash
# Run with current user permissions
ports

# Run with elevated permissions (recommended for full visibility)
sudo ports
```

**Recommended terminal size**: 120×30 or larger for optimal experience

### 🎮 Keyboard Controls

| Key | Action | Description |
|-----|--------|-------------|
| `q` | **Quit** | Exit the application |
| `u` | **Toggle Mode** | Switch between Unique and Detail views |
| `l` | **LISTEN Filter** | Show only listening sockets |
| `d` | **Docker Toggle** | Include/exclude Docker-published ports without host listeners |
| `+` / `-` | **Refresh Rate** | Increase/decrease update frequency |
| `a` | **Add Alias** | Create custom alias for selected row |
| `x` | **Delete Alias** | Remove alias from selected row |
| `g` | **Process Alias** | Set global alias for process type |
| `?` | **Help** | Show comprehensive help screen |
| `ESC` | **Close Help** | Return to main view from help |

### 📊 Display Modes

#### 🔹 **Unique Mode** (Default)
- **One line per port** with aggregated information
- Shows: Port number, state, process summary, container info
- **Best for**: Overview of active ports and quick identification

#### 🔹 **Detail Mode**
- **One line per process/container** mapping
- Shows: PID, user, full process name, connection details
- **Best for**: Debugging specific processes and connections

### 🏷️ **Alias System**

#### Per-Entry Aliases
- **Scope**: Specific to one row (process+PID+port in detail mode, port in unique mode)
- **Usage**: Press `a`, enter row number, provide custom name
- **Example**: Alias port 3000 as "Frontend Dev Server"

#### Per-Process Aliases
- **Scope**: All instances of a process name
- **Usage**: Press `g`, enter row number or process name, provide alias
- **Example**: Alias all "node" processes as "Node.js Applications"

#### Built-in Friendly Names
Automatic recognition for common services:
- `nginx` → "Web server"
- `mysqld` → "MySQL"  <!-- cspell:disable-line -->
- `redis-server` → "Redis"
- `docker-proxy` → "Docker published port"
- And many more...

## ⚙️ Configuration

### Port Range Configuration
Edit the constants at the top of the `ports` script:

```python
# Configuration section
LO_PORT, HI_PORT = 3000, 9999          # Port range to monitor
REFRESH_SECS_DEFAULT = 2.0              # Default refresh interval
ALIASES_PATH = "~/.ports_aliases.json"  # Alias storage location
```

### Common Port Ranges
```python
# Web development
LO_PORT, HI_PORT = 3000, 9999

# Full development range
LO_PORT, HI_PORT = 1024, 65535

# Common services only
LO_PORT, HI_PORT = 80, 8080
```

### Alias Storage
- **Location**: `~/.ports_aliases.json`
- **Format**: JSON with per-entry and per-process sections
- **Backup**: Automatic backup on corruption (`.bak` extension)
- **Sync**: Changes saved immediately

## 🐳 Docker Integration

### How It Works
1. **Container Detection**: Reads `docker ps` output for running containers
2. **Port Mapping**: Correlates host ports with container internal ports
3. **Metadata Display**: Shows container names, images, and port mappings
4. **State Indication**: Marks Docker-published ports as `PUBLISHED`

### Docker Features
- ✅ **Automatic detection** of Docker availability
- ✅ **Graceful fallback** when Docker is unavailable
- ✅ **Container correlation** with host processes
- ✅ **Port mapping visualization** (host:port → container:port/protocol)
- ✅ **Image and container name display**

### Docker Requirements
- Docker Desktop or Docker Engine running
- User permissions to run `docker ps` (or sudo access)

## 🔧 Troubleshooting

### Common Issues

| Issue | Solution |
|-------|----------|
| `Error: lsof not found` | Install lsof: `brew install lsof` (macOS) or `sudo apt install lsof` (Linux) |
| No ports shown | Check port range, press `l` to toggle LISTEN filter, try `sudo` for full visibility |
| Terminal display errors | Increase terminal size (min 80×24), reduce font size, or use larger window |
| Docker containers missing | Ensure Docker is running: `docker ps`, check container port mappings |
| Permission denied | Run with `sudo` for full process visibility |
| Slow performance | Reduce refresh rate with `-` key, check system load |

### Debug Commands
```bash
# Test lsof directly
lsof -nP -iTCP:3000-9999

# Test Docker integration
docker ps --format "{{.ID}} {{.Names}} {{.Image}} {{.Ports}}"

# Check Python version
python3 --version

# Verify script permissions
ls -la ports
```

### Performance Tips
- Use `sudo` only when needed for security
- Adjust port range to focus on relevant ports
- Increase refresh interval for better performance
- Close unused applications to reduce noise

## 🔒 Security Considerations

### Permissions
- **`sudo` access**: Allows reading all user processes via `lsof`
- **Docker access**: Requires permission to run `docker ps`
- **File system**: Creates `~/.ports_aliases.json` for alias storage

### What the Script Does
✅ **Safe operations**:
- Reads process information via `lsof`
- Queries Docker container status
- Displays parsed information in terminal UI
- Saves/loads alias configuration

❌ **Does NOT**:
- Modify running processes
- Open or close network ports
- Access network traffic content
- Modify system configuration
- Execute arbitrary commands

### Code Review
The script is fully open source. Key security points:
- Only executes `lsof` and `docker ps` commands
- No network connections initiated
- No system modifications performed
- All user input is validated and sanitized

## 🗑️ Uninstallation

### Remove System Installation
```bash
# Remove from system PATH
sudo rm -f /usr/local/bin/ports

# Remove from user PATH
rm -f "$HOME/bin/ports"

# Remove alias configuration (optional)
rm -f ~/.ports_aliases.json
```

### Clean PATH Configuration
```bash
# Remove PATH modification from shell config (if added)
# Edit ~/.bashrc or ~/.zshrc and remove the PATH export line
```

## 🤝 Contributing

We welcome contributions! Please see our contributing guidelines:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### Development Setup
```bash
git clone https://github.com/AdarBahar/ports.git
cd ports
chmod +x ports
./ports  # Test your changes
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### MIT License Summary
- ✅ Commercial use
- ✅ Modification
- ✅ Distribution
- ✅ Private use
- ❌ Liability
- ❌ Warranty

## 🙏 Acknowledgments

- Built with Python's `curses` library for terminal UI
- Uses `lsof` for system process information
- Docker integration via `docker ps` command
- Inspired by the need for better development port monitoring

---

**Made with ❤️ for developers who juggle multiple services and containers**
