# Dashboard

**Slug:** `dashboard`
**What it is:** Logged-in data views: metrics, tables, charts, filters, settings. The user is working, not browsing.
**Default aesthetic (brief is silent):** `swiss`

## Allowed aesthetics
- swiss
- dark-saas
- material
- flat
- mono-editorial
- enterprise
- glass (sparingly, panels only)
- minimalism

## Banned aesthetics
- every Retro, Raw, Illustrated, and Immersive aesthetic
- luxury
- art-deco
- neumorphism (fails contrast at data density)

## Must-have sections
- App shell: left sidebar (240px) or top bar, never both competing
- Page header with title, breadcrumb, primary action
- KPI row: 3 to 5 stat tiles
- Primary chart or table
- Secondary panels in a 2-column grid
- Filters as a horizontal bar above data, not a modal

## Layout skeleton
- Full-width fluid, no max-width; content fills the viewport
- Sidebar 240px collapsible to 64px icon rail
- Content gutter 24px
- Density setting: 8px row padding compact, 12px default
- Charts use the aesthetic's accent for the primary series and gray for context

## Component list
- Sidebar nav with active state
- Stat tile (label, value, delta)
- Data table with sortable headers, sticky first column
- Filter chip and date-range picker
- Empty state
- Toast

## Notes
- Tables and charts dominate; the aesthetic shows in chrome (nav, borders, type), not in data
- Load the `dataviz` skill for any chart, if it is available
- If the brief says 'admin' or 'internal', lean `swiss` or `flat`; if 'customer-facing analytics', lean `dark-saas` or `material`
