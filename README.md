# Design Website

Generate a premium one-page website mockup for a prospect using data from a Google Sheet.

This skill is built for fast outbound or pitch workflows: pull one prospect row, turn it into structured JSON, and generate a polished HTML mockup you can open locally.

## What It Does

- Reads a single prospect from a Google Sheet
- Normalizes flexible sheet column names into a predictable JSON shape
- Generates a self-contained HTML landing page
- Uses Unsplash images when available
- Falls back to placeholder imagery when no Unsplash key is configured

## Files

- [SKILL.md](/home/abdur-rafay/claude-code/.claude/skills/design-website/SKILL.md) - Claude skill instructions
- [scripts/read_prospect.py](/home/abdur-rafay/claude-code/.claude/skills/design-website/scripts/read_prospect.py) - Reads one row from Google Sheets and prints JSON
- [scripts/generate_website.py](/home/abdur-rafay/claude-code/.claude/skills/design-website/scripts/generate_website.py) - Reads JSON from stdin and writes an HTML mockup to `.tmp/`

## Workflow

1. Read a single prospect row from Google Sheets.
2. Pipe that JSON into the website generator.
3. Open the generated HTML file in a browser.

## Expected Prospect Fields

The sheet header matching is flexible. These names are normalized automatically:

- `company`, `company_name`, `organization_name` -> `company_name`
- `about`, `description`, `company_description` -> `description`
- `keywords`, `services`, `company_keywords` -> `keywords`
- `phone`, `phone_number`, `company_phone` -> `phone`
- `email`, `contact_email` -> `email`
- `address`, `full_address`, `company_address` -> `address`
- `city` -> `city`
- `state` -> `state`
- `country` -> `country`
- `industry`, `category` -> `industry`
- `first_name` -> `first_name`
- `last_name` -> `last_name`
- `title`, `role` -> `title`
- `website`, `company_website` -> `website`

## Requirements

- Python 3
- Google Sheets API access
- Google OAuth client credentials
- Python packages used by the scripts:
  - `python-dotenv`
  - `gspread`
  - `google-auth`
  - `google-auth-oauthlib`
  - `google-auth-httplib2`

## Auth Setup

### Google Sheets

The reader script looks for:

- `token.json` in the current working directory
- `credentials.json` in the current working directory
- or `GOOGLE_APPLICATION_CREDENTIALS` pointing to your credentials file

On first run, OAuth opens a local browser flow and then saves `token.json`.

### Unsplash

Set this in your `.env` file if you want real stock photos:

```env
UNSPLASH_ACCESS_KEY=your_key_here
```

If this key is missing, the generator uses `picsum.photos` placeholders instead.

## Usage

### Read one prospect

```bash
python3 .claude/skills/design-website/scripts/read_prospect.py \
  --url "GOOGLE_SHEET_URL" \
  --row 1
```

Optional worksheet selection:

```bash
python3 .claude/skills/design-website/scripts/read_prospect.py \
  --url "GOOGLE_SHEET_URL" \
  --row 1 \
  --worksheet "Sheet1"
```

### Generate a website directly from Sheets

```bash
python3 .claude/skills/design-website/scripts/read_prospect.py \
  --url "GOOGLE_SHEET_URL" \
  --row 1 | \
python3 .claude/skills/design-website/scripts/generate_website.py
```

### Generate from a saved JSON file

```bash
python3 .claude/skills/design-website/scripts/generate_website.py < prospect.json
```

## Output

The generator writes a file like:

```text
.tmp/website_company_name.html
```

The script also prints the output path after generation.

## Design Direction

The generated mockup follows the style documented in the skill:

- editorial, premium landing page feel
- off-white background
- bold uppercase typography
- serif italic supporting text
- strong image-driven hero
- simple bordered buttons

## Notes

- Row numbers are `1`-indexed and do not include the header row.
- Empty sheet values are skipped in the output JSON.
- If the selected row is out of range, the reader exits with an error.
- Generated HTML is self-contained except for remote images and Google Fonts.
