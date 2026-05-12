## Problem

The fixed top nav (~76px) plus the fixed "Choose your location" banner (~40px) sit on top of the hero, so the headline "WHERE SHARP MEN GET SHARPER" gets clipped/overlapped. The hero column also stacks too many elements (eyebrow tag + huge H1 + gold subtitle + paragraph + 2 buttons + 3 stats) into one tight area, which feels crowded.

## Goal

A calm, dynamic, breathable hero with zero overlap on any viewport.

## Changes (all in `src/routes/index.tsx`, hero section only)

1. **Fix the overlap**
   - Add `paddingTop: 120px` (desktop) / `100px` (mobile) to the hero content container so it always clears the fixed nav + location banner.
   - Switch hero from `height: 100vh` to `minHeight: 100vh` with flex centering, so content breathes instead of being jammed against the top.

2. **Declutter the copy stack**
   - Remove the eyebrow line `HAIRCUT • BEARD • SHAVE • GROOMING` (it duplicates the nav vibe and adds noise).
   - Keep H1 `WHERE SHARP MEN GET SHARPER` but reduce clamp to `clamp(48px, 8vw, 92px)` and tighten line-height.
   - Merge the gold subtitle + paragraph into a single shorter tagline: *"Dubai & Istanbul's premier barbershop — razor-edge precision for the modern man."*
   - Keep only the primary CTA `BOOK YOUR CHAIR`; demote `EXPLORE SERVICES` to a subtle text link with arrow.

3. **Move the stats bar out of the hero**
   - Lift the `2 / 15+ / 4.9★` row into its own thin band directly below the hero (dark surface, gold numerals, divided by hairlines). This is what makes the hero feel uncluttered while keeping the trust signals.

4. **Add subtle dynamism**
   - Slow Ken-Burns zoom on the background image (CSS keyframes, 20s scale 1 → 1.08).
   - Stagger fade-up via existing `Reveal` for: H1 → tagline → CTA, with 120ms offsets.
   - Soften the overlay gradient so the photo reads more clearly: `linear-gradient(180deg, rgba(10,10,10,0.75) 0%, rgba(10,10,10,0.45) 55%, rgba(10,10,10,0.85) 100%)`.

5. **Layout polish**
   - Constrain hero copy column to `maxWidth: 640px`.
   - Increase vertical rhythm: 24px between H1 and tagline, 36px before CTA.
   - Keep scroll-down chevron, but center it and lower its opacity.

## Out of scope

Nav, location banner, mobile menu, and all other sections stay untouched. No business logic, no new dependencies.
