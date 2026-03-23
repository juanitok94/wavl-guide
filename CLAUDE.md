# Haywood Hoppers — Claude Code Project Brief
> John Kean · Peachy Kean DevOps LLC · Asheville, NC
> Last updated: March 23, 2026

## What This Is
Haywood Hoppers is a mobile-first digital coffee passport
for Haywood Road, West Asheville, NC. 10 core stops,
east to west. Users walk the road, stamp each stop,
discover hidden collections. No auth, no login,
localStorage only.

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
| 1 | Cooperative Coffee Roasters | South |
| 2 | BattleCat Coffee Bar | North |
| 3 | Flora | South |
| 4 | Haywood Famous | South |
| 5 | Bad Manners Coffee | North |
| 6 | Dobra Tea West | North |
| 7 | Rowan Coffee | North |
| 8 | Odd's Cafe | South |
| 9 | Plant Bar | South |
| 10 | Izzy's Coffee House | South |

## Bonus/Directory Stops
- Firestorm Books & Coffee (Hygge Five anchor, Prague 1993)
- Asheville Kava X Coffee (demoted — gas station adjacent)
- Deep Time Coffee (demoted — open only 4 days/week)

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

## Current Build Status (March 23, 2026)
- ✅ Homepage
- ✅ Passport page
- ✅ Stop pages (individual)
- ✅ Map page with flip toggle
- ✅ Mobile-first card upgrade
- ✅ Copy wordsmith pass (ChatGPT)
- ⬜ shops.json restructure (Flora, Dobra as core)
- ⬜ streetSide field added to all shops
- ⬜ Stop page I-240 zone label fix
- ⬜ BottomNav
- ⬜ Progressive disclosure on stop pages
- ⬜ Share button on stop pages
- ⬜ ChatGPT content for Flora, Dobra, Bad Manners
- ⬜ Dark mode (post user testing)
- ⬜ Shop photos (after photo walk)
- ⬜ Progress visualization on passport page
