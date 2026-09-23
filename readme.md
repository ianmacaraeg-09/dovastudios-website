# DOVA — landing page

Single self-contained file. Nothing to build, nothing to install.

## Deploy to Netlify

**Drag and drop:** go to app.netlify.com → Sites → drag this whole folder
(or the zip) onto the drop area. Live in about ten seconds.

**Custom domain:** Site configuration → Domain management → Add a domain,
then point your DNS at Netlify. Done.

## What's in here

- `index.html` — the whole landing page: markup, CSS, JS, every image and the
  DOVA logo inlined. ~1.8 MB, one request.
- `discover.html` — the discovery flow the "Book a demo" buttons lead to.
  Five questions, then a blueprint assembled from the answers. Also self-contained.
- `_headers` — a couple of sensible security headers. Safe to delete.

There is deliberately no `netlify.toml` and no build config: this is a static
drop, so Netlify should run no build step and no plugins at all. If a deploy
ever fails with a plugin error, check Site configuration → Build & deploy →
Build settings and clear the build command, then remove anything under
Build plugins.

## External dependencies (2, both optional)

- **Outfit** (Google Fonts) — stands in for Ataero Retina OB Edition. To swap
  in the licensed font, add an `@font-face` rule and change `--font` in `:root`.
- **GSAP 3.12.5 + ScrollTrigger** (cdnjs) — preloader, hero parallax, scroll
  reveals. If it fails to load the page still renders completely; it just
  doesn't animate. The agent orbs, activity feed and number counters are
  plain JS and never depend on it.

## Editing

Design tokens sit at the top of the `<style>` block:

    --parchment  #e5e4e0   page canvas
    --ink        #1d1d1d   text
    --paper      #ffffff   card surfaces
    --ash        #bfbebe   hairlines
    --stone      #cdcdc9   agent-section panel
    --gradient-sphere      hero gradient

**Agent orbs** — palettes live in the `PALETTES` object in the orb script.
Add an agent by adding a palette entry and an element with
`class="orb" data-orb="<key>"`.

**Client logos** (the 3D marquee) — each tile is a 480x320 image on
`.ref .lg-XX` with its background colour on `.ref.brand-XX`.

**Service illustrations** — `.viz.pic img`, one per preset card.

## Echo chat widget

Inlined directly into `index.html`'s existing `<script>`/`<style>` blocks (not
a separate file) — reuses the page's own orb-drawing code and its real
`PALETTES` object (hoisted out of the orb IIFE so there's one source of truth
for agent colors, not two). Bubble bottom-right, opens into a small chat
panel; real backend, real TTS (Fish Audio, server-side).

**Endpoint is currently local dev only**: `http://127.0.0.1:8821/chat`, DOVA's
own Echo instance (`github.com/ianmacaraeg-09/dovastudios-ai-agents`). Not
reachable from this file once it's actually deployed to Netlify — swapping in
a real public endpoint (persistent Cloudflare Tunnel, once that's set up) is
a one-line change to `ECHO_ENDPOINT` near the top of the widget's script
block. See the "Echo Live Deployment Plan" artifact for the full go-live
checklist (Mac mini/Hermes, the tunnel, the Claude LLM swap).

## Before you go live

- Pricing figures (₱24,999 / ₱2,500 / ₱7,999 / ₱6,499 / ₱4,999 / ₱29,999)
- `hello@dova.ph` — not a real address yet
- The Payments card still mentions BIR-compliant series
- Section 01 artwork for Payments and Inventory shows Nomos and Kora, who are
  not in the six-agent roster
