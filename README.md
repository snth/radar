# radar

**Finger protocol** (RFC 1288) re-imagined for the **AT Protocol (atproto) / Bluesky** ecosystem

## The Finger Connection

In the early days of the internet, the `finger` command let users scan a remote server to view a person's real-time availability, log-in status, or custom profile snippet (via local `.plan` files). 

As the web centralized, Finger faded away. `radar` reboots this concept for the modern federated web. Instead of pinging a centralized server, it scans decentralized personal data repositories to pull a user's latest broadcasted status (their most recent post) using public AT Protocol endpoints.

## Features

*   **Zero Dependencies:** Simple POSIX shell script using only curl, awk, and sed.  Works out of the box on Linux, macOS, and BSD.
*   **Permissionless:** Read-only lookups. No authentication, API keys, or App Passwords required.
*   **Flexible Formatting:** Accepts both modern Bluesky handles (`user.bsky.social`) and classic finger-style email formats (`user@bsky.social`).

## Installation & Usage

1. Clone or download the script:
   ```bash
   curl -O https://raw.githubusercontent.com/snth/radar/refs/heads/main/radar
   chmod +x radar
   ```

2. Scan a user:
   ```bash
   ./radar snth.bsky.social
   # Or using classic finger style:
   ./radar snth@bsky.social
   ```

## How It Works

1. **Normalizes** the input handle (converts `@` delimiters to `.`).
2. **Resolves** the public handle to a Decentralized Identifier (DID) via the AT Protocol Identity endpoints.
3. **Fetches** the most recent record from the actor's public feed using native string parsing.

