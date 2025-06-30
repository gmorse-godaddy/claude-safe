# claude-safe

A wrapper script that allows you to run Claude Code in dangerous mode safely within a Docker container on macOS and WSLv2.

## Overview

`claude-safe` provides a secure way to use Claude Code's dangerous mode by isolating it within a Docker container. This gives you the power of dangerous mode while protecting your host system from potentially harmful operations.

## Features

- Runs Claude Code in a Docker container with dangerous mode enabled
- Supports both macOS and WSLv2 environments
- Automatically mounts your current directory into the container
- Preserves your Claude Code configuration and settings
- Provides network isolation options
- Handles file permissions correctly between host and container

## Requirements

- Docker installed and running
- Claude Code CLI (`claude`)
- macOS or Windows with WSLv2

## Installation

1. Clone this repository:
   ```bash
   git clone git@github.com:jgowdy-godaddy/claude-safe.git
   ```

2. Make the script executable:
   ```bash
   chmod +x claude-safe
   ```

3. Add the script to your PATH or create an alias:
   ```bash
   # Option 1: Copy to a directory in your PATH
   cp claude-safe /usr/local/bin/

   # Option 2: Create an alias in your shell profile
   alias claude-safe='/path/to/claude-safe'
   ```

## Usage

```
Usage: claude-safe [OPTIONS]

Options:
  -l, --lang, --language <lang>  Specify language/platform (can be used multiple times)
  -h, --help                     Show this help message

Supported languages:
  python  - Python with pip, poetry, virtualenv
  go      - Go with go modules support
  rust    - Rust with cargo
  dotnet  - .NET Core/.NET 5+
  node    - Node.js with npm, yarn, pnpm
  java    - Java with Maven and Gradle
  ruby    - Ruby with bundler
  php     - PHP with composer
```

### Examples

```bash
# Auto-detect language based on files in current directory
claude-safe

# Specify a single language
claude-safe --lang python

# Specify multiple languages
claude-safe --lang python --lang go

# Short form with multiple languages
claude-safe -l rust -l python -l node

# Pass through Claude Code arguments
claude-safe --continue

# Work with files in your current directory
cd /path/to/project
claude-safe
```

The script will automatically:
- Start a Docker container with Claude Code installed
- Mount your current directory
- Install language-specific tools based on your selection or auto-detection
- Run Claude Code in dangerous mode
- Clean up the container when you're done

## How It Works

The script creates an isolated Docker environment where Claude Code can operate in dangerous mode without risking damage to your host system. Your working directory is mounted into the container, allowing Claude to read and modify files as needed while keeping the operations sandboxed.

## Security Considerations

While this script provides isolation through Docker, remember that:
- Files in your mounted directory can still be modified
- Network access may be available depending on your Docker configuration
- Always review changes made by Claude before committing them

## Platform-Specific Notes

### macOS
- Requires Docker Desktop for Mac
- File permissions are handled automatically

### WSLv2
- Requires Docker Desktop with WSL2 backend enabled
- Ensure your project files are within the WSL2 filesystem for best performance

## Contributing

Feel free to submit issues and pull requests to improve this tool.

## License

This project is provided as-is for the community's benefit.