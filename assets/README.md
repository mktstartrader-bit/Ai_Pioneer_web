# Assets

These files were extracted from the inlined base64 data URIs in `index.html`. They are kept here as the canonical source so that future edits don't require base64-decoding the HTML.

The deployed site still serves the inlined versions inside `index.html` — these files are **not loaded at runtime**. They are reference / source-of-truth copies.

## Inventory

All images live in [`images/`](images/).

| File | Bytes | Format | Used in `index.html` | Purpose |
|---|---:|---|---|---|
| `favicon-32.png` | 1,297 | PNG | Line 11 | 32×32 browser tab favicon |
| `apple-touch-icon.png` | 6,137 | PNG | Line 12 | 180×180 iOS home-screen icon |
| `hero-bg.webp` | 406,472 | WebP | Lines 123, 664 | Hero `background-image`; reused as the Judges section background |
| `logo-startrader.webp` | 4,670 | WebP | Lines 1090, 1379 | STARTRADER wordmark — appears in the topbar and footer |
| `hero-model.webp` | 100,042 | WebP | Line 1114 | Masked-model photo in the hero right column |
| `judge-peter-karsten.webp` | 85,746 | WebP | Line 1283 | Peter Karsten portrait in the Judges section |

Two of the base64 blobs in `index.html` are duplicates (the hero background is reused for the Judges section, and the STARTRADER logo is reused in the footer) — only the unique files are stored here.

## (Optional) `icons/` folder

Empty. Reserved for any SVG icons we later choose to extract out of `index.html` (currently they live inline in the `PILLARS` array and in the hero/strip markup).

## Updating the inlined HTML from these files

If you replace one of these files, you also need to re-inline the new bytes into `index.html`. Quick script:

```bash
# Example: replace the hero model image
python3 - <<'PY'
import base64, pathlib, re
html_path = pathlib.Path("index.html")
img_bytes = pathlib.Path("assets/images/hero-model.webp").read_bytes()
new_data_uri = "data:image/webp;base64," + base64.b64encode(img_bytes).decode()
html = html_path.read_text()
# Match the <img class="model" src="..."> line and replace its src
html = re.sub(
    r'(<img class="model" src=")data:image/[^"]+(")',
    lambda m: m.group(1) + new_data_uri + m.group(2),
    html,
    count=1,
)
html_path.write_text(html)
PY
```

Adapt the selector and target file for each asset.

## Re-running the extraction

The script at `/tmp/extract_assets.py` (created during the doc scaffolding) finds every `data:image/...;base64,...` URI in `index.html`, decodes it, and writes a deduplicated set to `assets/images/`. If you regenerate, the files will be re-named with hash-suffixed defaults (e.g. `asset_01_098a90ee.png`) — rename them back to the semantic names in the table above.
