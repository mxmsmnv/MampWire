# MampWire Agent Instructions

This folder is a MAMP Pro ProcessWire local installation helper.

## Goal

When the user asks to install ProcessWire, install the latest ProcessWire `dev` branch into the current MAMP site folder and create a local credentials file.

## Environment

MAMP Pro manages:

- the local domain
- the web server
- the document root
- PHP versions in the GUI

The agent manages:

- downloading ProcessWire dev
- creating the database through MAMP MySQL CLI
- running the ProcessWire CLI installer
- saving local credentials

## Defaults

Use these MAMP defaults unless the user provides different values:

```txt
MySQL CLI: /Applications/MAMP/Library/bin/mysql
MySQL host: 127.0.0.1
MySQL port: 8889
MySQL user: root
MySQL password: root
ProcessWire branch: dev
Site profile: site-blank
Admin user: admin
```

Detect the MAMP PHP binary from:

```txt
/Applications/MAMP/bin/php/php*/bin/php
```

Prefer the newest available version.

## Installation Command

If the user gives a domain, run:

```bash
bash bin/mampwire-install --domain USER_DOMAIN
```

If the user gives a database name too, run:

```bash
bash bin/mampwire-install --domain USER_DOMAIN --db-name USER_DB_NAME
```

If `bin/mampwire-install` is missing, create or restore it from this repository before continuing.

## Safety Rules

- Treat the current working directory as the MAMP site document root.
- Do not delete existing user files unless the user explicitly asks.
- Do not use `--force` unless the user explicitly asks to reinstall over an existing ProcessWire copy.
- Do not commit `.local/admin.md`.
- If the folder already contains `site/assets/installed.php`, stop and report that ProcessWire appears installed.
- If MySQL is not reachable, ask the user to start MAMP servers.

## Credential Output

After a successful install, make sure this file exists:

```txt
.local/admin.md
```

It should include:

- site URL
- admin URL
- admin user
- generated admin password
- database host
- database port
- database name
- database user
- database password

## Expected Result

The site should open at:

```txt
https://USER_DOMAIN/
```

The admin should open at the URL shown in `.local/admin.md`.
