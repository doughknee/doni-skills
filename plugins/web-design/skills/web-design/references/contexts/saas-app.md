# SaaS App

**Slug:** `saas-app`
**What it is:** Logged-in product UI that is not primarily data: editors, forms, settings, inboxes, boards, workflows.
**Default aesthetic (brief is silent):** `dark-saas`

## Allowed aesthetics
- dark-saas
- material
- flat
- swiss
- mono-editorial
- glass
- neumorphism (consumer apps only)
- bento (overview and home screens)
- minimalism
- playful (consumer or edu apps)

## Banned aesthetics
- Retro family
- Raw family
- photo-led
- motion-first
- luxury
- art-deco
- maximalism

## Must-have sections
- App shell with sidebar or top nav
- Primary work surface (editor, board, list)
- Detail pane or drawer
- Settings pages with grouped form sections
- Onboarding and empty states
- Command palette (⌘K) when the aesthetic is dark-saas or mono-editorial

## Layout skeleton
- Fluid full-width shell; content panes have their own max-width (720px for forms)
- Three-pane layouts: nav 240px, list 320px, detail fluid
- Form sections: label above input, 16px vertical rhythm, 24px between groups
- Modals max 560px wide

## Component list
- Sidebar with collapsible groups
- Form field with label, help text, error
- Select, combobox, toggle, checkbox
- Modal and drawer
- Inline editable text
- Avatar and presence dot
- Keyboard shortcut hint

## Notes
- Interaction states (hover, focus, active, disabled) matter more here than anywhere else; every recipe's A11y block applies
- Prefer the aesthetic's `--surface` ladder for pane separation over borders when it has one
