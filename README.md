# Alkoteka Scraper Scaffold

This repository contains a Scrapy project for parsing products from alkoteka.com.

## Requirements
- Python 3.10+
- Scrapy 2.11+

## Setup

1.  **Create and activate a virtual environment:**

    ```bash
    python3 -m venv .venv
    source .venv/bin/activate
    ```

2.  **Install dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

3.  **Install pre-commit hooks:**

    ```bash
    pre-commit install
    ```

## Configuration

The spider can be configured via `config.ini` or Command Line Interface (CLI) arguments.

### `config.ini`
The default configuration is stored in `config.ini`:
```ini
[spider]
base_url = https://alkoteka.com
categories_file = categories.txt
```

### Category File Format
The category file (default: `categories.txt`) should contain one URL or path per line.
- **Full URLs:** `https://alkoteka.com/catalog/vino`
- **Relative Paths:** `/catalog/vino` (will be appended to `base_url`)

Example:
```text
https://alkoteka.com/catalog/krepkiy-alkogol
/catalog/vino
/catalog/shampanskoe-i-igristye-vina
```

## Running the Spider

### Standard Run
Uses defaults from `config.ini`.
```bash
scrapy crawl alkoteka -O result.json
```

### CLI Overrides
You can override configuration values using the `-a` flag.

**Change category file:**
```bash
scrapy crawl alkoteka -a categories=my_custom_list.txt -O result.json
```

**Change base URL:**
```bash
scrapy crawl alkoteka -a base_url=https://mirror.alkoteka.com -O result.json
```

**Combine overrides:**
```bash
scrapy crawl alkoteka -a categories=dev_list.txt -a base_url=https://dev.alkoteka.com -O result.json
```

## Notes
- Proxy support and region handling (Krasnodar) are partially implemented (region cookie is forced).
