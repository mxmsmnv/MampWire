# MampWire

MampWire is a small local installer recipe for creating ProcessWire development sites inside MAMP Pro.

It assumes you create the MAMP Pro site/domain manually, then let Codex or another coding agent install ProcessWire into that site's document root.

## What It Does

- Uses the ProcessWire `dev` branch.
- Creates a MySQL database through the MAMP CLI.
- Downloads and extracts ProcessWire.
- Runs the ProcessWire CLI installer.
- Saves local admin/database credentials to `.local/admin.md`.

## Requirements

- macOS
- MAMP Pro 7.4.3 or newer
- MAMP servers running
- A MAMP Pro site already created and pointed at the folder where you run the installer
- `curl`, `unzip`, and the MAMP MySQL/PHP binaries

## Quick Start

Open a terminal in the MAMP site folder and run:

```bash
bash bin/mampwire-install --domain example.test
```

Optional database name:

```bash
bash bin/mampwire-install --domain example.test --db-name example_test
```

The installer writes credentials to:

```txt
.local/admin.md
```

## MAMP Defaults

The script defaults to common MAMP settings:

```txt
MySQL host: 127.0.0.1
MySQL port: 8889
MySQL user: root
MySQL password: root
```

You can override them:

```bash
bash bin/mampwire-install \
  --domain example.test \
  --mysql-port 3306 \
  --mysql-user root \
  --mysql-pass root
```

## Agent Workflow

1. Create a site in MAMP Pro.
2. Point the site document root to your project folder.
3. Copy or clone this repository into that folder.
4. Open the folder in Codex.
5. Ask Codex:

```txt
Install ProcessWire dev using MampWire. Domain: example.test
```

Codex should read `AGENTS.md` and run the installer.

## Notes

The installer refuses to run if ProcessWire appears to already be installed unless you pass `--force`.

Use this for local development only. The generated credential file is intentionally ignored by git.
