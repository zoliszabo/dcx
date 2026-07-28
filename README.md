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
# Show the selected container for the current directory
dcx

# Run a command in the matching container
dcx python app.py

# Run a command in a specific Compose service
dcx --service web sh
```
