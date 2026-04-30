# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

# Haywood Hoppers — Claude Code Project Brief
> John Kean · Peachy Kean DevOps LLC · Asheville, NC
> Last updated: March 27, 2026

## What This Is
Haywood Hoppers is a mobile-first digital coffee passport
for Haywood Road, West Asheville, NC. 10 core stops,
east to west. Users walk the road, stamp each stop,
discover hidden collections. No auth, no login,
localStorage only.

## Commands

```bash
npm run dev        # Start local dev server at localhost:3000
npm run build      # Production build
npm run lint       # ESLint (Next.js config)
npx tsc --noEmit   # Type-check without emitting (required before finishing any task)
```

No test suite exists. Manual review at localhost:3000 is the test process.

## Live URLs
- Production: wavl-guide.vercel.app
- Repo: github.com/juanitok94/wavl-guide
- Local: localhost:3000 (npm run dev in C:\wavl-guide)

## Tech Stack
- Next.js 16 App Router
- TypeScript (strict)
- Tailwind CSS 4
- localStorage for all user state
- Vercel for deployment (auto-deploy on git push)

## Design Principles — Non-Negotiable
1. Hygge — warmth, slowness, belonging
2. Camino — journey, earned progress, east to west
3. Krug — don't make me think, clarity first
4. Mobile-first — primary user is holding a phone
   on Haywood Road. Desktop is graceful enhancement only.
5. Human first — if it feels like a generic app,
   it's wrong. It should feel like West Asheville.

## Color System — Do Not Change
- Parchment background: #f5edd8
- Espresso dark: #3b1f0a
- Gold accent: #c8973a
- Rust primary: #6b3f1e
- Body text: #1a1208

## Typography — Do Not Change
- Playfair Display — headings (font-serif)
- Crimson Pro — body text (font-serif)
- IBM Plex Mono — labels, UI elements (font-mono)

## Two ICPs
1. TOURISTS — visiting Asheville, want authentic local
   experiences, not chains, not tourist traps.
   Respond to discovery, walking, feeling like an insider.
2. BUSINESS OWNERS — independent shop owners on Haywood
   who want foot traffic and to feel proud of being
   featured, not marketed at.

## The 10 Core Stops (east to west)
| # | Shop | Street Side |
|---|------|-------------|
| 1 | Cooperative Coffee Roasters | North |
| 2 | BattleCat Coffee Bar | South |
| 3 | Flora & Forage | North |
| 4 | Haywood Famous | North |
| 5 | Bad Manners Coffee | South |
| 6 | Rowan Coffee | South |
| 7 | Odd's Cafe | North |
| 8 | Plant Bar | South |
| 9 | Izzy's Coffee House | North |
| 10 | West End Bakery | South |

## Bonus/Directory Stops
- Firestorm Books & Coffee (Hygge Five anchor, Prague 1993)
- Asheville Kava X Coffee (demoted — gas station adjacent)
- Deep Time Coffee (demoted — open only 4 days/week)

## Honorable Mentions
- Dobra Tea West (strong candidate — tea-forward, excellent vibe)
- Potential New Boyfriend

## Core Stop Eligibility Rule
A shop must be open minimum 5 days per week to qualify
as a core passport stop. Coffee or tea as primary mission.

## The Hygge Five
A hidden collection of 5 stops where time slows down.
Currently under revision — do not modify hygge flags
in shops.json without confirming with John first.

## File Structure
src/
  app/
    page.tsx          — homepage
    map/page.tsx      — interactive map
    passport/         — stamp collection
    stop/[slug]/      — individual stop pages
  data/
    shops.json        — canonical data, source of truth
    layers.json       — map filter layers
    badges.json       — achievement badges
    trivia.json       — trivia questions per stop
  lib/
    stamps.ts         — localStorage stamp logic

## shops.json Data Shape

Key fields on each shop object:

| Field | Type | Notes |
|-------|------|-------|
| `id` | string | kebab-case slug, used in URL and image paths |
| `passportType` | `"core"` \| `"bonus"` \| absent | core = numbered passport stop |
| `passportStop` | number | 1–10, east-to-west order |
| `zone` | `"north"` \| `"south"` | **GOTCHA: "north" = East Haywood (before I-240); "south" = West Haywood (past I-240)**. The passport page labels these "North of I-240" / "South of I-240" — confusing but intentional geographic labeling |
| `coordinates` | `[lon, lat]` | longitude first (not lat/lon) |
| `selloColor` | hex | per-shop accent color for stamp circles and headers |
| `layers` | string[] | e.g. `["coffee"]` — used for map filter visibility |
| `hygge` | boolean | Hygge Five membership — do not modify without confirmation |
| `hours` | `{ mon–sun: string, note?: string }` | `"Closed"` for closed days |
| `stamp` | `{ welcomeLine, subLine }` | Shown after stamping on stop page |
| `story` | `{ headline, body, insiderTip?, parkingNote? }` | Editorial content |

### Image paths on stop pages

`/stop/[slug]/page.tsx` loads images as `/images/shops/{shop.id}.jpg` (no suffix).
The naming convention (`{id}-exterior.jpg`) is for the photo library — when adding
real photos, you need **both** a bare `{id}.jpg` (for the stop page hero) and
the named variants. The bare `{id}.jpg` is the primary image.

### Client vs. Server components

- `app/page.tsx` — server component (no `'use client'`, no localStorage)
- `app/map/page.tsx` — `'use client'` (uses stamps, useState)
- `app/passport/page.tsx` — `'use client'` (uses stamps, useState)
- `app/stop/[slug]/page.tsx` — `'use client'` (uses stamps, useState)

All stamp reads must be guarded: `lib/stamps.ts` returns `{}` during SSR.
Never call stamp functions outside `useEffect` or client components.

## Standing Rules for Claude Code
1. Always check TypeScript compiles before finishing
   (npx tsc --noEmit)
2. Never modify shops.json stop numbers or core/bonus
   status without explicit confirmation from John
3. Never change colors, fonts, or design tokens
4. Mobile-first — test layout at 390px width thinking
5. Always localhost review before git push
6. Commit message format:
   feat: for new features
   fix: for corrections
   refactor: for restructuring
7. Data mapping — when mapping values to shops or stops,
   always verify against the source table above; never
   assume geographic order matches stop number order
8. Truncated messages — if a message appears cut off,
   complete the task based on available context; only ask
   for clarification if the intent is genuinely ambiguous

## Current Build Status (March 28, 2026)
- ✅ Homepage
- ✅ Passport page
- ✅ Stop pages (individual)
- ✅ Map page with flip toggle
- ✅ Mobile-first card upgrade
- ✅ Copy wordsmith pass (ChatGPT)
- ✅ streetSide field added to all shops
- ✅ Share button on stop pages
- ✅ Progressive disclosure on stop pages
- ✅ Shop photo zone with FPO fallback
- ✅ Stop page I-240 zone label fix
- ✅ Map bottom sheet popup with spring animation
- ✅ Photo naming convention established
- ✅ First shop owner contact (Eva, Haywood Famous)
- ✅ Travel writer outreach (Kayleigh Ruller, Eater/Condé Nast)
- ✅ Billy Cooley connection (Downtown Asheville Association)
- ⬜ shops.json restructure (Flora, Dobra as core)
- ⬜ BottomNav
- ⬜ ChatGPT content for Flora, Dobra, Bad Manners
- ⬜ Dark mode (post user testing)
- ⬜ Shop photos (after photo walk)
- ⬜ Progress visualization on passport page

## Photo Library
Photos location: public/images/shops/
Naming convention: {shop-id}-exterior.jpg,
{shop-id}-interior.jpg, {shop-id}-interior-2.jpg

### Current Inventory
- flora-forage-exterior.jpg ✅
- flora-forage-interior.jpg ✅
- flora-forage-interior-2.jpg ✅
- flora-forage-interior-3.jpg ✅
- haywood-famous-exterior.jpg ✅
- haywood-famous-interior.jpg ✅
- owl-bakery-exterior.jpg ✅
- owl-bakery-interior.jpg (FPO) ✅
- cooperative-coffee-roasters-exterior.jpg ✅
- cooperative-coffee-roasters-interior.jpg (FPO) ✅

### Still Needed
- battlecat-coffee-bar-exterior.jpg
- battlecat-coffee-bar-interior.jpg
- bad-manners-coffee-exterior.jpg
- bad-manners-coffee-interior.jpg
- rowan-coffee-exterior.jpg
- rowan-coffee-interior.jpg
- odds-cafe-exterior.jpg
- odds-cafe-interior.jpg
- plant-bar-exterior.jpg
- plant-bar-interior.jpg
- izzys-coffee-house-exterior.jpg
- izzys-coffee-house-interior.jpg
- west-end-bakery-exterior.jpg
- west-end-bakery-interior.jpg
- haywood-famous-interior.jpg

## Lab Notes Protocol

When you make a mistake or take a wrong approach, automatically append a lab note to this CLAUDE.md under ## Lab Notes without being asked. Format:
[date] - what failed - why - what to do instead.

## Lab Notes

- 2026-03-27 - mapped streetSide values by stop number order — geographic position does not match stop number order on Haywood Road; always verify against the explicit shop table in this file

