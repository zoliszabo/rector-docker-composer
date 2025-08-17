# Rector Docker Composer Package

A Composer-based wrapper for running [Rector](https://getrector.com/) via Docker. This package provides a convenient way to use Rector without requiring PHP or Rector to be installed locally on your system.

## What is this?

This Composer package provides a `rector-docker` command that wraps the [zoliszabo/rector-docker](https://github.com/zoliszabo/rector-docker) Docker image, making it easy to run Rector on your PHP projects through a simple command-line interface.

## Key Benefits

- **No local PHP installation required** - Run Rector regardless of your system's PHP version
- **Always up-to-date** - Uses the latest Rector version from the Docker image
- **Cross-platform compatibility** - Works on any system that supports Docker
- **Intelligent terminal detection** - Automatically handles interactive vs non-interactive environments
- **Simple integration** - Drop-in replacement for the standard `rector` command

## Installation

### Global Installation (Recommended)

Install the package globally to use the `rector-docker` command from anywhere:

```bash
composer global require zoliszabo/rector-docker
```

Make sure your global Composer `bin` directory is in your system's `PATH`. You can find the path with:

```bash
composer global config bin-dir --absolute
```

### Project-specific Installation

You can also install it as a development dependency in your project:

```bash
composer require --dev zoliszabo/rector-docker
```

## Usage

Once installed, navigate to your project directory and use `rector-docker` exactly like you would use the regular `rector` command:

```bash
# Process using default rector.php configuration
rector-docker process

# Process your src directory
rector-docker process src

# Show available rules
rector-docker list-rules

# Generate a rector.php configuration file
rector-docker init

# Dry run to see what would be changed
rector-docker process src --dry-run

# Process with a specific configuration file
rector-docker process src --config custom-rector.php
```

All arguments and options are passed directly to Rector running inside the Docker container.

## How it Works

The `rector-docker` command:

1. Detects if it's running in an interactive terminal environment
2. Mounts your current working directory to `/app` inside the Docker container
3. Runs the appropriate `docker run` command with the correct flags
4. Forwards all your arguments to Rector inside the container

### Interactive vs Non-Interactive Detection

The script automatically detects the environment:

- **Interactive terminals**: Uses `-it` flags for proper terminal interaction
- **CI/Scripts**: Omits `-it` flags to prevent hanging in non-interactive environments

## Requirements

- Docker installed and running on your system
- Composer for package installation

## Docker Image

This package uses the `zoliszabo/rector:latest` Docker image, which contains:

- Latest PHP version
- Latest Rector version
- All necessary dependencies

## Related Projects

- [rector-docker](https://github.com/zoliszabo/rector-docker) - The underlying Docker image
- [Rector](https://getrector.com/) - The PHP refactoring tool

## License

MIT License. See [LICENSE](LICENSE) file for details.

## Contributing

Issues and pull requests are welcome!
