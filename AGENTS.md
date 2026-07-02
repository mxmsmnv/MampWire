# MampWire Agent Instructions

This folder is a MAMP Pro ProcessWire local installation helper.

## Goal

When the user asks to install ProcessWire, install the latest ProcessWire `dev` branch into the current MAMP site folder and create a local credentials file.

If the user message contains only a link to this repository, treat that as a request to install ProcessWire dev into the current working directory. Do not wait for a more explicit command.

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
MySQL CLI: auto-detect from /Applications/MAMP/Library/bin/mysql and mysql*/bin/mysql
MySQL host: 127.0.0.1
MySQL port: read from /Applications/MAMP/tmp/mysql/my.cnf when available, otherwise 8889 then 3306
MySQL user: root
MySQL password: root
ProcessWire branch: dev
Site profile: site-blank
Admin user: same value as the generated database name unless the user provides one
Admin path: generated from Irish names unless the user provides one
Generated passwords: lowercase letters, uppercase letters, and digits only
```

Detect the MAMP PHP binary from:

```txt
/Applications/MAMP/bin/php/php*/bin/php
```

Prefer the newest available version.

## Installation Command

Preferred link-only workflow:

1. Treat the current working directory as the MAMP site document root.
2. If this repository is not already present in the current folder, clone or download it to a temporary folder outside the site root.
3. Run the installer from the temporary copy and point it at the current folder:

```bash
bash /path/to/MampWire/bin/mampwire-install --root "$PWD"
```

The installer will try to infer the domain from the generated MAMP Pro Apache/Nginx config by matching the current folder to a MAMP document root.

If the user gives a domain, run:

```bash
bash bin/mampwire-install --domain USER_DOMAIN
```

If the user gives a database name too, run:

```bash
bash bin/mampwire-install --domain USER_DOMAIN --db-name USER_DB_NAME
```

If `bin/mampwire-install` is missing, create or restore it from this repository before continuing.

If the installer cannot infer the domain, ask the user for the MAMP domain. This is the only expected blocking question in the link-only workflow.

## Safety Rules

- Treat the current working directory as the MAMP site document root.
- Do not delete existing user files unless the user explicitly asks.
- Do not use `--force` unless the user explicitly asks to reinstall over an existing ProcessWire copy.
- Do not commit `.local/admin.md`.
- If the folder already contains `site/assets/installed.php`, stop and report that ProcessWire appears installed.
- If MySQL is not reachable on the configured port, check `/Applications/MAMP/tmp/mysql/my.cnf`; if no port is available there, try port `3306` before asking the user to start MAMP servers.

## Reporting Problems

The user's Mac is expected to have the GitHub CLI (`gh`) available.

If installation fails because of a MampWire bug, missing MAMP layout support, unclear ProcessWire CLI behavior, or another reusable issue in this project, create a GitHub issue in `mxmsmnv/MampWire` before ending the task:

```bash
gh issue create \
  --repo mxmsmnv/MampWire \
  --title "Short failure summary" \
  --body "What failed, the command that was run, sanitized output, detected MAMP/PHP/MySQL paths, and what was expected."
```

Do not include generated passwords, API keys, private customer data, full database dumps, or contents of `.local/admin.md` in the issue.

After creating the issue, tell the user the issue URL and the immediate workaround if one is known.

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
https://DETECTED_OR_USER_DOMAIN/
```

The admin should open at the URL shown in `.local/admin.md`.
