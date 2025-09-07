# 🚀 Ports Manager

A powerful, feature-rich terminal-based tool for monitoring network ports and processes on macOS and Linux. Built for developers working with multiple services, containers, and microservices. Now with **automatic updates**, **advanced alias system**, and **professional-grade user experience**.

![Ports Manager Demo](https://img.shields.io/badge/Platform-macOS%20%7C%20Linux-blue)
![Python Version](https://img.shields.io/badge/Python-3.8%2B-green)
![License](https://img.shields.io/badge/License-MIT-yellow)
![SPDX License](https://img.shields.io/badge/SPDX--License--Identifier-MIT-blue)
![Version](https://img.shields.io/badge/Version-2.1.1-brightgreen)
![Auto Update](https://img.shields.io/badge/Auto--Update-✅-success)

## ✨ Features

### 🔄 **Automatic Update System** ⭐ *NEW*
* **Smart version checking** on startup against GitHub releases
* **One-click updates** with automatic download and restart
* **Safe update process** with backup and rollback protection
* **Non-blocking checks** that don't delay application startup
* **Version display** in header for immediate visibility

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

### 🎨 **Professional UI/UX**
* **Color-coded connection states** (LISTEN, ESTABLISHED, PUBLISHED)
* **Responsive layout** that adapts to terminal size
* **Comprehensive help system** with ESC key support
* **Intuitive keyboard shortcuts** for all operations
* **Terminal resize protection** during user input
* **Debounced key handling** for smooth interaction

### 🏷️ **Advanced Alias System** ⭐ *ENHANCED*
* **Per-entry aliases**: Custom names for specific port/process combinations (24 chars)
* **Per-process aliases**: Global friendly names for process types
* **Built-in friendly names** for common services (nginx, MySQL, Redis, etc.)
* **Persistent storage** with automatic backup and recovery
* **Smart character limiting** with visual feedback
* **Truncation support** for legacy long aliases

### ⚡ **Performance Optimized**
* **Compiled regex patterns** for maximum parsing speed
* **Efficient data structures** with proper typing
* **Minimal memory footprint** and CPU usage
* **Robust error handling** with graceful degradation
* **Configurable timeouts** for external commands

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

# Check version and auto-update status
ports --version

# Get comprehensive help
ports --help

# Skip auto-update check
ports --no-update
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
| `+` / `-` | **Refresh Rate** | Increase/decrease update frequency (0.2s - 10.0s) |
| `a` | **Add Alias** | Create custom alias for selected row (max 24 chars) |
| `x` | **Delete Alias** | Remove alias from selected row |
| `g` | **Process Alias** | Set global alias for process type |
| `?` | **Help** | Show comprehensive help screen |
| `ESC` | **Cancel/Close** | Cancel current operation or close help |

### 💻 Command Line Options

| Option | Description |
|--------|-------------|
| `--version`, `-v` | Show version information and exit |
| `--help`, `-h` | Display comprehensive help and usage |
| `--no-update` | Skip automatic update check on startup |

### 📊 Display Modes

#### 🔹 **Unique Mode** (Default)
- **One line per port** with aggregated information
- Shows: Port number, state, process summary, container info
- **Best for**: Overview of active ports and quick identification

#### 🔹 **Detail Mode**
- **One line per process/container** mapping
- Shows: PID, user, full process name, connection details
- **Best for**: Debugging specific processes and connections

### 🏷️ **Advanced Alias System** ⭐ *ENHANCED*

#### Per-Entry Aliases
- **Scope**: Specific to one row (process+PID+port in detail mode, port in unique mode)
- **Character Limit**: 24 characters with smart input limiting
- **Usage**: Press `a`, enter row number, provide custom name
- **Visual Feedback**: Shows character limit and validates input
- **Example**: Alias port 3000 as "Frontend Dev Server"

#### Per-Process Aliases
- **Scope**: All instances of a process name
- **Usage**: Press `g`, enter row number or process name, provide alias
- **Persistent**: Applies to all current and future instances
- **Example**: Alias all "node" processes as "Node.js Applications"

#### Built-in Friendly Names
Automatic recognition for common services:
- `nginx` → "Web server"
- `mysqld` → "MySQL"  <!-- cspell:disable-line -->
- `redis-server` → "Redis"
- `docker-proxy` → "Docker published port"
- `postgres` → "PostgreSQL"
- `java` → "Java app"
- And many more...

#### Alias Features ⭐ *NEW*
- **Smart truncation** for display (shows ellipsis for long aliases)
- **Input validation** with retry loops and clear error messages
- **ESC key cancellation** for all alias operations
- **Confirmation feedback** showing what was saved/deleted
- **Automatic persistence** with backup and recovery

## 🔄 **Automatic Update System** ⭐ *NEW FEATURE*

### How It Works
- **Startup Check**: Automatically checks GitHub for newer versions when you start the app
- **Smart Comparison**: Uses semantic versioning (major.minor.patch) for accurate updates
- **User Choice**: Shows clear prompt with version info - you decide whether to update
- **Safe Process**: Creates backup before update, restores if anything goes wrong

### Update Process
1. **Start Application** → Automatic version check (non-blocking)
2. **If Update Available** → See prompt with current vs. latest version
3. **Press 'u'** → Download, backup, install, and restart automatically
4. **Press any other key** → Continue with current version

### Update Prompt Example
```
🚀 UPDATE AVAILABLE

Current version: 2.1.0
Latest version:  2.1.1

A newer version of Ports Manager is available!

Press 'u' to update automatically
Press any other key to continue with current version
```

### Safety Features
- **Automatic backup** of current version before update
- **Rollback protection** - restores backup if download fails
- **Timeout protection** - won't hang on slow connections
- **Graceful fallback** - app works even if update check fails
- **Non-blocking** - doesn't delay startup if GitHub is slow

### Version Display
- **Header shows version** - `Ports Manager by Adar Bahar v2.1.1`  <!-- cspell:disable-line -->
- **Instant visibility** - see your current version immediately
- **No command needed** - version always visible in interface

## ⚙️ Configuration

### Port Range Configuration
Edit the constants at the top of the `ports` script:

```python
# Configuration section
VERSION = "2.1.1"                       # Current version (auto-managed)
LO_PORT, HI_PORT = 3000, 9999          # Port range to monitor
REFRESH_SECS_DEFAULT = 2.0              # Default refresh interval
COMMAND_TIMEOUT_SECS = 10.0             # Timeout for external commands
ALIASES_PATH = "~/.ports_aliases.json"  # Alias storage location
MAX_ALIAS_LENGTH = 24                   # Maximum alias character length
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
| **Auto-update not working** | Check internet connection, repository may be private, use `--no-update` to skip |
| **Update prompt not showing** | Ensure you're running older version, check GitHub releases page |
| **Update download fails** | Check network connectivity, GitHub may be down, backup is automatically restored |
| **Input not working (double chars)** | Terminal compatibility issue, try different terminal or update terminal app |
| **Aliases not saving** | Check file permissions for `~/.ports_aliases.json`, may need write access |

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

## 🆕 What's New in v2.1.1

### ⭐ **Major Features Added**
- **🔄 Automatic Update System** - One-click updates with safe backup/restore
- **📱 Version Display** - Current version shown in header at all times
- **🏷️ Enhanced Alias System** - 24-character limit with smart input validation
- **⌨️ Professional Input Handling** - ESC key support, proper backspace, no double characters
- **🎯 Improved User Experience** - Debounced keys, terminal resize protection, inline error messages

### 🔧 **Technical Improvements**
- **Robust Error Handling** - Comprehensive validation and graceful degradation
- **Performance Optimization** - Efficient data structures and compiled regex patterns
- **Code Quality** - Proper typing, modular design, comprehensive documentation
- **CLI Interface** - `--version`, `--help`, `--no-update` command-line options

### 📊 **Version Comparison**

| Feature | v1.x | v2.0.x | v2.1.x |
|---------|------|--------|--------|
| Auto-updates | ❌ | ❌ | ✅ |
| Version display | ❌ | ❌ | ✅ |
| Alias character limit | 18 | 18 | 24 |
| Input validation | Basic | Basic | Advanced |
| ESC key support | ❌ | ❌ | ✅ |
| CLI options | ❌ | Basic | Full |
| Error handling | Basic | Good | Excellent |
| Code quality | Good | Very Good | Excellent |

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

# Test auto-update (temporarily change VERSION to older number)
# Test with different scenarios
ports --version
ports --help
ports --no-update
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

- Built with Python's `curses` library for professional terminal UI
- Uses `lsof` for comprehensive system process information
- Docker integration via `docker ps` command for container monitoring
- GitHub API integration for seamless auto-update functionality
- Inspired by the need for better development port monitoring tools
- Designed for developers working with complex microservice architectures

## 🌟 Star History

If you find Ports Manager useful, please consider giving it a star on GitHub! ⭐

## 📈 Project Stats

- **Language**: Python 3.8+
- **Dependencies**: Zero external dependencies (uses only standard library)
- **Platform Support**: macOS, Linux
- **License**: MIT (fully open source)
- **Auto-Updates**: ✅ Fully automated
- **Code Quality**: Professional grade with comprehensive error handling

---

**Made with ❤️ for developers who juggle multiple services and containers**

*Ports Manager v2.1.1 - The professional way to monitor your development ports*
