# dcx

`dcx` is a small helper for running commands inside the Docker Compose container that matches your current working directory.

## What it does

When you run `dcx` from a project directory, it:

- finds the relevant Compose project,
- detects the running container whose bind mount contains your current directory, and
- runs your command in that container with the matching working directory.

## Requirements

- Docker Compose v2 (`docker compose`)
- `jq`

## Installation

Copy the script somewhere in your `PATH`, for example:

```bash
chmod +x dcx

# Global installation (system-wide)
sudo install dcx /usr/local/bin/dcx

# User-only installation (current user)
install dcx ~/.local/bin/dcx
```

You can also run it directly from the repository checkout.

## Usage

```bash
# Show the version or help (works outside a Compose project)
dcx --version
dcx --help

# Show the selected container for the current directory
dcx

# Run a command in the matching container
dcx python app.py

# Start Bash in the matching container
dcx bash

# Run a command in a specific Compose service
dcx --service web sh
```

## Locales

`dcx` forwards nonempty host `LANG`, `LANGUAGE`, `LC_ALL`, and `LC_CTYPE`
variables to the command in the container. If `LANG`, `LC_ALL`, and `LC_CTYPE`
are all empty or unset, it passes `LANG=C.UTF-8` as a UTF-8 default.

The forwarded locale must be available in the image. If your host uses a locale
that the container does not provide, override it with one the image supports:

```bash
LC_ALL=C.UTF-8 dcx bash
```

`C.UTF-8` is available in many common images, but availability depends on the
image. Install or generate another locale in the image if needed.
