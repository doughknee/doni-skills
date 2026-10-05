# Documentation

**Slug:** `docs`
**What it is:** Reference and guides: sidebar tree, search, code blocks, versioning, API tables.
**Default aesthetic (brief is silent):** `mono-editorial`

## Allowed aesthetics
- mono-editorial
- swiss
- minimalism
- dark-saas
- material

## Banned aesthetics
- everything else

## Must-have sections
- Top bar: logo, search, version switcher, theme toggle
- Left sidebar: nested tree with current page highlighted
- Content: title, description, body, prev/next
- Right rail: on-this-page TOC (desktop only)
- Code blocks with copy button and language tab

## Layout skeleton
- Three-column: sidebar 260px, content fluid max 760px, TOC 220px
- Mobile: sidebar becomes drawer, TOC hidden
- Body 16px, line-height 1.6
- Code 14px mono
- Headings get anchor links on hover

## Component list
- Sidebar tree
- Search (⌘K)
- Code block with tabs
- Callout (note, warning, tip)
- API table (param, type, default, description)
- Prev/next footer
- Breadcrumb

## Notes
- Light mode default with a dark toggle; `dark-saas` flips that
- Callouts use the recipe's semantic colors; if it has none, use #0070f3 info, #f5a623 warning, #ee0000 error
