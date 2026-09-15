EPEC Field Documentation

Technician-facing field reference docs, published as bookmarkable web pages via GitHub Pages. No login required — pages are reachable only by direct link (this repo is public but unlisted; there's no search engine indexing or public directory of pages beyond the index below).

Live site: https://epecsupport.github.io/Service/

Current pages
Page	Source file
EPEC Field Documentation	index.md
3WA / ETU600	3WA.md
3WA / ETU600 (Español)	3WA_ES.md
Hardware List	hardware.md
Contacts	contacts.md
Adding a new page
Create a new .md file at the repo root. Avoid spaces in the filename — use hyphens (e.g. 3VA-Information.md), since spaces get URL-encoded and are easy to mistype on a phone.
Start the file with front matter — this is required for the page to render through the custom layout instead of being served as a raw, unstyled file:
   ---
   layout: default
   title: Your Page Title
   ---
Write content in standard markdown. A few things specific to this site:
Tables need a blank line before them. Text immediately followed by a table (no blank line) gets swallowed into one paragraph and the pipes render as literal characters instead of a table.
Emails and phone numbers are NOT auto-linked except on contacts.md (see below). Elsewhere, link them manually: [name@epec.com](mailto:name@epec.com) or [555-1234](tel:5551234).
External links (anything off this domain) automatically open in a new tab — no extra markup needed.
Commit to main. GitHub Pages rebuilds automatically, usually live within a minute or two.
If you want the page discoverable from the homepage, add a link to it in index.md.
Repo structure
_config.yml         — kramdown configured for GFM-style markdown (tables, etc.)
_layouts/
  default.html       — shared page template: favicon/home-screen icon tags,
                        light/dark mode CSS, table styling, and the two
                        scripts described below
assets/               — favicon and iOS/Android home-screen icon set
                        (generated via a favicon generator; see naming
                        convention below)
index.md, *.md        — the actual doc pages
Behavior baked into the layout (_layouts/default.html)
Home screen icon: iOS "Add to Home Screen" uses assets/apple-icon-precomposed.png. Note: iOS caches this at the moment a page is added to a home screen — updating the image later won't refresh existing shortcuts. Users need to remove the icon, clear Safari's site data, and re-add it.
Light/dark mode: follows the phone's system setting automatically via prefers-color-scheme — no toggle, no configuration needed per page.
External links open in a new tab automatically (any link whose host differs from this site's).
Auto-linking of emails/phone numbers only runs on pages whose URL path contains "contacts" (currently just contacts.md). This is intentionally scoped — the detection regex could otherwise mislink part numbers or quantities in the hardware tables.
Known constraints
Pages are public. Access control is "unlisted URL," not authentication — don't add sensitive or customer-specific data without reconsidering this model.
The repo name (Service) is used in absolute asset paths (/Service/assets/...) inside _layouts/default.html. Renaming the repo requires updating those paths too.
