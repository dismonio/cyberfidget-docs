# Cyber Fidget Docs

Documentation for **Cyber Fidget**: setup, hardware, and app development.  
Built with **MkDocs + Material** for a fast, dark, search-powered docs site.

## TL;DR
```bash
# 1) Create & activate a venv
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

# 2) Install deps
pip install -r requirements.txt

# 3) Run local preview
mkdocs serve
# Open the URL it prints (usually http://127.0.0.1:8000)

# 4) Publish (CI does this on push to main)
mkdocs gh-deploy --force    # optional manual deploy
```

---

## Prereqs
- Python 3.9+ recommended  
- `pip` available in PATH  
- (Optional) A GitHub repo set up with Pages

---

## Repo layout
```
docs/                    # All markdown lives here
  index.md               # Landing page
  getting-started/
    overview.md
    first-flash-arduino.md
    first-flash-circuitpython.md
  hardware/
    specs.md
    pinout.md
  software/
    apps.md
    storage.md
    ota-builder.md
  assets/                # Images & downloads (create as needed)

mkdocs.yml               # Nav, theme, and site config
requirements.txt         # mkdocs + theme dependencies
.github/workflows/docs.yml  # CI: build & publish to GitHub Pages
README.md
```

---

## Writing guidelines

**Audience:** people curious at a booth + early adopters + reviewers + devs.

- Keep the **landing pages acronym-light**. Expand on first use (e.g., “Wi-Fi/Bluetooth (BLE)”).
- Prefer **short sections**, lists, and code blocks. Avoid long walls of text.
- Use **Material callouts**:
  ```markdown
  !!! tip "Quick tip"
      Short, actionable guidance.
  ```
- Link internally with relative paths:
  ```markdown
  See [Pinout](../hardware/pinout.md).
  ```
- Images go in `docs/assets/`; reference with relative paths:
  ```markdown
  ![CF close-up](../assets/cf-close.jpg)
  ```
- Add “Tested on hardware rev X” notes for examples when relevant.

---

## Navigation
`mkdocs.yml` controls the sidebar/top tabs. Add pages to the `nav:` tree, for example:
```yaml
nav:
  - Home: index.md
  - Getting started:
    - Overview: getting-started/overview.md
    - First flash (Arduino): getting-started/first-flash-arduino.md
```

---

## Local development
```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

pip install -r requirements.txt
mkdocs serve
```
- The site auto-reloads on save.  
- Keep an eye on terminal warnings for broken links.

---

## Deployment

### CI (recommended)
This repo includes `.github/workflows/docs.yml`. On **push to `main`** (changes in `docs/**`, `mkdocs.yml`, or `requirements.txt`), GitHub Actions:
1. Installs deps  
2. Builds the site  
3. Publishes to the `gh-pages` branch

### Custom domain
1. In your DNS, create a **CNAME**:
   - **Host**: `docs`
   - **Value**: `<your-github-username>.github.io`
2. In repo **Settings → Pages → Custom domain**: `docs.cyberfidget.com`  
   GitHub will manage the `CNAME` file on the `gh-pages` branch.

---

## Style & theme
Configured in `mkdocs.yml`:
```yaml
theme:
  name: material
  palette:
    - scheme: slate
      primary: cyan
      accent: cyan
features:
  - navigation.tabs
  - navigation.sections
  - content.code.copy
  - content.tabs.link
  - toc.integrate
markdown_extensions:
  - admonition
  - attr_list
  - def_list
  - footnotes
  - md_in_html
  - pymdownx.details
  - pymdownx.superfences
  - pymdownx.highlight
  - toc:
      permalink: true
```

---

## Common tasks

**Add a page**
1. Create a `.md` file under `docs/…`
2. Add it to `nav` in `mkdocs.yml`
3. `mkdocs serve` to preview

**Add images**
- Put under `docs/assets/...`
- Reference with `![alt](../assets/file.png)`

**Link to the main site / buy page**
- Use full URLs:  
  `https://cyberfidget.com/`  
  `https://cyberfidget.com/buy.html`

---

## Troubleshooting

- **Build fails in CI**
  - Check `docs.yml` logs in the Actions tab.
  - Run locally: `mkdocs build --strict` to catch warnings as errors.

- **404 after adding a page**
  - Make sure it’s listed in `nav:` and the path is correct.

- **Broken image**
  - Confirm the relative path from the referencing page.
  - Filenames are case-sensitive on GitHub Pages.

- **Custom domain not working**
  - DNS can take time to propagate.  
  - Verify CNAME points to `<username>.github.io`.  
  - Re-save the custom domain setting to regenerate certificates.

---

## Contributing

- Keep PRs small and focused.
- Use clear headings, code blocks, and callouts.
- Don’t introduce acronyms on landing pages without expanding first.
- Add screenshots/GIFs for app examples when possible.

---

## License
Docs content: © Cyber Fidget.  
(If you prefer a specific open license for docs, add it here—e.g., CC BY-SA.)
