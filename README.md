# d2txt (Directory to Text)

A Python script that converts a directory structure into a single text file, preserving file contents and directory hierarchy while respecting `.gitignore` rules.

## Features

- Scans directory recursively and outputs contents as a single text file
- Respects `.gitignore` rules (both global and subdirectory-specific)
- Handles negative patterns in `.gitignore` (patterns starting with `!`)
- Automatically excludes binary files
- Generates unique delimiters to separate files
- Supports custom exclude patterns via command line arguments
- Debug mode for troubleshooting
- **Perfect for AI Language Model Context**: The output format is ideal for providing codebase context to AI language models like Gemini, Claude, etc., allowing them to understand and work with entire project structures within their context windows

## Use Cases

### General Use
- Creating text backups of project structures
- Sharing code in text-only environments
- Documenting project states

### AI Development
- Providing full codebase context to AI language models
- Enabling AI models to understand project structure and relationships between files
- Facilitating code review and analysis with AI assistants
- Perfect for long-context models (like Claude, Gemini) that can process large amounts of code context

## Default Excludes

The following patterns are excluded by default:
- `.git`
- `.gitignore`
- `*.pyc`
- `__pycache__`
- `node_modules`

## Installation

No installation required. Just download `d2txt.py` and make it executable:

```bash
chmod +x d2txt.py
```

## Usage

Basic usage:
```bash
./d2txt.py /path/to/directory
```

With additional exclude patterns:
```bash
./d2txt.py /path/to/directory -e "*.log" -e "*.tmp"
```

Enable debug output:
```bash
./d2txt.py /path/to/directory --debug
```

### Using with AI Language Models

1. Generate the text representation of your project:
```bash
./d2txt.py /path/to/project > project_context.txt
```

2. Use the generated file as context in your prompts to AI language models. The clear delimiter format helps models understand the project structure and file relationships.

Example prompt:
```
I have a project with the following structure and contents:

[paste contents of project_context.txt]

Could you [your question about the codebase]?
```

## Output Format

The script generates a text file with the following format:

```
# Project Directory Contents
# Format: Files are separated by a delimiter line starting with "### FILE_[uuid] "
# Each delimiter line is followed by the file path, then the file contents.
# Note: Binary files and patterns matching any .gitignore are excluded.

# DELIMITER=### FILE_[uuid] 

### FILE_[uuid] path/to/file1.txt
[contents of file1.txt]

### FILE_[uuid] path/to/file2.txt
[contents of file2.txt]
```

## Technical Details

### GitignoreRule Class
- Handles individual `.gitignore` rules
- Supports pattern matching with proper scope handling
- Processes directory-specific patterns
- Handles negation patterns

### GitignoreHandler Class
- Manages multiple `.gitignore` rules
- Applies rules in correct order
- Handles rule precedence and negation

## Requirements

- Python 3.7 or higher
- Standard library modules only (no external dependencies)

## License

[MIT License](https://opensource.org/licenses/MIT)

## Contributing

Feel free to open issues or submit pull requests if you find any bugs or have suggestions for improvements.