# Clash Rules

This repository contains Clash proxy rules for various domains and services.

## Files

- `Proxy-Domain.list` - Domain suffix rules for proxy routing
- `Direct-Domain.list` - Domain suffix rules for direct routing  
- `Proxy-CIDR.list` - IP CIDR rules for proxy routing
- `Direct-CIDR.list` - IP CIDR rules for direct routing
- `Proxy-Process.list` - Process rules for proxy routing
- `Direct-Process.list` - Process rules for direct routing

## Scripts

### extract_domains.py

A Python script to extract wildcard domains from ZeroOmega Gist configuration and append them to `Proxy-Domain.list`.

#### Usage

```bash
python3 extract_domains.py
```

#### Requirements

```bash
pip install requests
```

#### Features

- Fetches ZeroOmega configuration from GitHub Gist
- Extracts wildcard domain patterns from "auto switch" profile
- Converts wildcard patterns (*.domain.com) to DOMAIN-SUFFIX format
- Automatically deduplicates existing entries
- Appends new domains to Proxy-Domain.list

#### Configuration

The script is configured to fetch from:
- Gist URL: https://gist.github.com/cloud-native-yang/1d4db297fd0146b850f51e33143a4fa5
- Target file: Proxy-Domain.list

To modify the source or target, edit the variables in the `main()` function.

## GitHub Actions Workflow

The repository includes a GitHub Actions workflow (`.github/workflows/main.yml`) that automatically:

1. **Extracts domains**: Runs the `extract_domains.py` script to fetch and append new domains from the ZeroOmega Gist
2. **Creates rule providers**: Converts the `.list` files to Clash YAML format
3. **Commits changes**: Automatically commits and pushes the updated rules

### Workflow Triggers

- **Manual trigger**: Can be run manually via GitHub Actions UI
- **Push to main**: Automatically runs when changes are pushed to the main branch

### Workflow Steps

1. Checkout repository
2. Set up Python 3.10
3. Install Python dependencies (requests)
4. Extract domains from ZeroOmega Gist
5. Create Clash rule providers
6. Commit and push changes
