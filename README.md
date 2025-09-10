# PyPI Search Tool Documentation

A reliable command-line tool for searching Python packages on PyPI using official APIs.

## Overview

This tool was created to solve the common problem of broken PyPI search utilities. Unlike tools like `pip_search` and `pypi-search` that rely on web scraping (which breaks when PyPI updates their website), this tool uses PyPI's official JSON API for reliable, stable searches.

## Features

- 🔍 **Reliable search** using PyPI's official JSON API
- 📦 **Exact match detection** with detailed package information
- 🔢 **Configurable result limits** with sensible defaults
- 🚀 **Fast and lightweight** with minimal dependencies
- 🛡️ **Future-proof** - won't break when PyPI updates their website
- 📋 **Rich package details** including version, author, license, and links

## Installation

1. Save the script as `pypi_search` (or any name you prefer)
2. Make it executable:
   ```bash
   chmod +x pypi_search
   ```
3. Optionally, add it to your PATH for global access

## Usage

### Basic Search
```bash
./pypi_search <package_name>
```

### Examples

#### Default search (shows up to 10 results)
```bash
./pypi_search flask
```

#### Limit results to 5
```bash
./pypi_search flask -l 5
```

#### Show all results (no limit)
```bash
./pypi_search flask -l 0
```

#### Search with verbose output
```bash
./pypi_search django -v
```

## Command Line Options

| Option | Description | Default |
|--------|-------------|---------|
| `query` | Package name or search term (required) | - |
| `-l, --limit` | Maximum number of results to show | 10 |
| `-v, --verbose` | Show more detailed output | False |
| `-h, --help` | Show help message | - |

### Limit Options
- **Default (10)**: `./pypi_search numpy`
- **Custom limit**: `./pypi_search numpy -l 5`
- **No limit**: `./pypi_search numpy -l 0`

## Output Format

The tool provides two types of results:

### 1. Exact Match (if found)
```
✅ Exact match found:
📦 flask
   Version: 2.3.3
   Summary: A simple framework for building complex web applications.
   Author: Armin Ronacher
   License: BSD-3-Clause
   Homepage: https://palletsprojects.com/p/flask
   Repository: https://github.com/pallets/flask
   Install: pip install flask
```

### 2. Related Packages
```
📋 Showing 10 of 45 packages containing 'flask' (use -l 0 for all results):

1. flask-admin
   Summary: Simple and extensible admin interface framework for Flask
   Version: 1.6.1
   Install: pip install flask-admin

2. flask-login
   Summary: User authentication and session management for Flask.
   Version: 0.6.3
   Install: pip install flask-login
```

## Use Cases

### Finding a specific package
```bash
./pypi_search requests
```

### Exploring available packages
```bash
./pypi_search machine-learning -l 20
```

### Quick package verification
```bash
./pypi_search beautifulsoup4
```

### Finding alternatives
```bash
./pypi_search http-client -l 15
```

## Technical Details

### Dependencies
- Python 3.6+
- `requests` library
- `argparse` (built-in)
- `urllib.parse` (built-in)

### API Endpoints Used
- **Exact match**: `https://pypi.org/pypi/{package_name}/json`
- **Package listing**: `https://pypi.org/simple/`

### How It Works
1. **Exact Match**: Uses PyPI's JSON API to fetch detailed information for exact package name matches
2. **Similar Packages**: Parses PyPI's simple package index to find packages containing the search term
3. **Package Details**: Fetches detailed information for each matching package using the JSON API

## Troubleshooting

### Common Issues

#### "No packages found"
- Check your spelling
- Try broader search terms
- Use the web interface fallback URL provided

#### Timeout errors
- Check your internet connection
- The tool has built-in timeouts (10s for exact match, 15s for package listing)

#### Permission denied
- Make sure the script is executable: `chmod +x pypi_search`
- Check file permissions

### Error Handling
The tool gracefully handles:
- Network timeouts
- API unavailability
- Invalid package names
- Missing package information

## Integration Tips

### Add to PATH
```bash
# Add to your ~/.bashrc or ~/.zshrc
export PATH="$PATH:/path/to/your/script/directory"
```

### Create an alias
```bash
# Add to your ~/.bashrc or ~/.zshrc
alias pysearch='/path/to/pypi_search'
```

### Use in scripts
```bash
#!/bin/bash
packages=("requests" "flask" "django")
for pkg in "${packages[@]}"; do
    echo "Checking $pkg..."
    ./pypi_search "$pkg" -l 1
done
```

## Comparison with Other Tools

| Tool | Status | Method | Reliability |
|------|--------|---------|-------------|
| `pip_search` | ❌ Broken | Web scraping | Low |
| `pypi-search` | ❌ Broken | Web scraping | Low |
| `pip-pss` | ⚠️ Variable | Web scraping | Medium |
| **This tool** | ✅ Working | Official API | High |

## Contributing

### Potential Improvements
- Add package download statistics
- Include package classification information
- Add package dependency information
- Support for searching by author or maintainer
- Color output support
- JSON output format option

### Reporting Issues
If you encounter any issues:
1. Check that you have the latest version
2. Verify your internet connection
3. Test with a known package name like "requests"
4. Check PyPI's status at https://status.python.org/

## License

This tool is provided as-is for educational and practical use. Feel free to modify and distribute according to your needs.

---

**Note**: This tool provides a reliable alternative to broken PyPI search utilities by using official APIs rather than fragile web scraping methods.

