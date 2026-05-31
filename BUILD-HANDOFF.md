# Flamingo PDP — Build Handoff

**Date:** 2026-05-30 · **Build target:** 2026-05-31
**Goal:** Ship the **Series Three — Project Flamingo** PDP as a sibling of the live Peacock page, reusing the same design system so the two read as one brand family. Differentiated by **colorway (pink)**, **core (Velocity Hybrid Core)**, and **no lifetime / "Backed for Life" messaging**.

**Peacock template (source of truth for design + structure):** `~/code/proton-peacock-pdp-preview/` (live at https://tonyflo79.github.io/proton-peacock-pdp-preview/, deploys from `main`).
**Project source (copy doc, compose scripts, paddle renders):** `~/code/client-work/copywriting-business/clients/proton-sports/`.

---

## 0 · TL;DR approach

1. Clone the Peacock repo → new Flamingo repo (or sibling page).
2. Change **only the accent color** in CSS (teal/purple → flamingo pink). Everything else in the design system stays identical = brand consistency.
3. Find/replace SKU identity (Peacock → Flamingo) and core (**Atomic Foam Core → Velocity Core**).
4. **Rewrite** the durability/warranty-dependent parts (Flamingo is a *pop & feel* paddle, not a *durability + lifetime warranty* paddle). This is the real work — see §1 and §5.
5. Regenerate the 9 product images from the existing **Flamingo Pink** renders using the same compose scripts (already font-size-tuned for mobile).
6. Verify desktop + mobile (headless), commit, push, deploy.

The brand logo (Proton atom), fonts, layout, components, pros 2×2 grid, mobile feature-ordering, and logo placements all carry over **unchanged**.

---

## 1 · The positioning difference (READ FIRST — everything flows from this)

| | **Peacock (live)** | **Flamingo (to build)** |
|---|---|---|
| Core | **Atomic (Foam) Core** — dense, consistent solid foam | **Velocity (Hybrid) Core** — foam + polypropylene honeycomb hybrid |
| Story | **Durability** + consistency | **Pop, feel, liveliness** — "the liveliest paddle in the lineup" |
| Warranty | **Lifetime Warranty on Construction** / "Backed for Life" | **Different / shorter — NOT lifetime** (confirm term — see gate #1). Drop "Backed for Life." |
| Accent | Teal → purple (`--peacock`) | Flamingo **pink** |
| Pros | Jade, Genie, Andre, Pablo | **Genie, Augie Ge, Jalina Ingram** (+confirm 4th) |

**SHARED verbatim across both** (one construction platform): AeroGrade Construction™, aerospace grade carbon fiber (full phrase), roughness enhanced / structurally integrated, dual-stamp UPA + USA Pickleball at the legal max, Elongated/Wide-Body shapes, 13mm/15mm thickness, founder Charles Darling.

**Rule of thumb:** anywhere the Peacock copy leans on *durability* or *lifetime/Backed-for-Life*, the Flamingo must pivot to *pop / feel / liveliness* + its own (shorter) warranty. Everywhere it talks *construction platform*, it stays the same.

Velocity Core canonical description (from Messaging System v2 §"The Lineup" + Mechanism table):
> The Flamingo is the **Velocity Core** paddle — a **foam-and-honeycomb hybrid** built for **pop and feel**, the liveliest paddle in the Proton lineup. Two materials engineered together: **solid foam for power, polypropylene honeycomb for springy responsiveness.**

---

## 2 · OPEN QUESTIONS — confirm with Mike before/while building (GATES)

1. **Flamingo warranty term** — #1 trap. NOT lifetime. What is it exactly (e.g., limited 1–2yr "warranty on construction"? standard manufacturer warranty)? Every warranty string + the §4 feature row + FAQ #2 + footer depend on this.
2. **Prices** — Flamingo Elongated / Wide-Body, and prior-retail/relaunch framing. (Peacock: Elongated **$195** / Wide-Body **$175**, was ~~$280~~.)
3. **Pro lineup** — photos exist for **Genie Bouchard, Augie Ge, Jalina Ingram**. Confirm the full 4 (is Genie shared with Peacock, or Flamingo-only? who is the 4th?).
4. **Velocity Core image source** — need a "core-only" render (foam + honeycomb cutaway) analogous to Peacock's `Peacock-Core.png`, for the split cutaway image (02). If none, fall back to the Tech-Specs render or a finished-face-only core image. (See §7.)
5. **Colorway accent** — **Pink** is primary; a **Blue** Flamingo colorway also exists. Confirm the pink gradient (candidate in §4).
6. **§6 Counter ("What If It's Your Paddle?")** — Peacock's counter is a *durability/degradation* argument; it does **not** fit Flamingo's pop/feel story. Drop it, or replace with a pop/feel counter (e.g., "Want more pop without losing control?"). Confirm.
7. **Tour-credit FAQ** — we removed FAQ #6 from Peacock. Assume removed for Flamingo too unless Mike says otherwise.
8. **Hero anchor** — what replaces "Backed for Life" in the Flamingo H1 / close (e.g., "Built for Pop & Feel" / "The Liveliest Paddle")?

---

## 3 · Repo / build setup

**Recommended:** new GitHub Pages repo `proton-flamingo-pdp-preview` mirroring Peacock (clean separate preview URL).

```bash
# from ~/code
cp -R proton-peacock-pdp-preview proton-flamingo-pdp-preview
cd proton-flamingo-pdp-preview
rm -rf .git && git init -b main
git mv assets/peacock assets/flamingo            # rename asset dir
# update index.html image paths assets/peacock/ -> assets/flamingo/
# (then create the GitHub repo + push; enable Pages on main)
```

*(Alternative: a `flamingo.html` + `assets/flamingo/` inside the existing Peacock repo if Mike prefers one repo. The standalone repo keeps the two cleanly separated and gives Flamingo its own preview link.)*

---

## 4 · Design-system deltas (CSS) — change ONLY the accent

The template, fonts (Hanken Grotesk + Clash Display), dark surfaces, components, spacing, pros 2×2, mobile feature-ordering, logo placements: **all identical**. Change just these `:root` vars in `index.html`:

| Var | Peacock (now) | Flamingo (candidate — Mike to tune) |
|---|---|---|
| `--cy` | `#5FD5E0` (cyan) | `#FF6FA5` (flamingo pink) |
| `--teal` | `#2CE5C7` | `#FF8FB0` |
| `--peacock` (gradient, rename to `--flamingo`) | `linear-gradient(96deg,#2CE5C7 0%,#3FC8E6 24%,#3E7BF0 52%,#7B4BEC 78%,#C457DD 100%)` | `linear-gradient(96deg,#FF9CC0 0%,#FF6FA5 26%,#FF4D7D 54%,#E84393 78%,#C0399B 100%)` |
| `--hair-2` | `rgba(95,213,224,0.34)` | `rgba(255,111,165,0.34)` |

Then global find/replace `var(--peacock)` → `var(--flamingo)` (used by `.grad`, `.kicker::before`, `.btn`, `.brand .dot` if present, seam lines). The atom logo PNG stays — it's brand-level, not SKU. This is the "branding consistency": same everything, pink accent instead of teal.

> Note: image-baked accents (the cyan callout/subtitle text + cyan seam in the 9 product images) come from the **compose scripts'** `CYAN = (95,213,224)` constant. For full consistency, change that to the flamingo pink RGB in each script when regenerating (see §7).

---

## 5 · Section-by-section map (SAME / SWAP / REWRITE)

Peacock structure (in `index.html`, top→bottom). Action key: **KEEP** = verbatim; **SWAP** = find/replace SKU identity + colorway image; **REWRITE** = real copy change (durability→pop/feel or warranty).

| # | Section | Action | Notes |
|---|---|---|---|
| NAV | brand + links + utility | **KEEP** | Identical (Proton atom logo, same links). |
| — | Breadcrumb | **SWAP** | "Project Peacock" → "Project Flamingo". |
| 1 | **HERO** buy box | **SWAP + REWRITE** | Eyebrow: Peacock→Flamingo. **H1** rewrite: `Aerospace Technology. Velocity Core. Optimized Spin. [Flamingo anchor]` (drop "Backed for Life" — gate #8; gradient on "Velocity Core. Optimized Spin."). **Deck** rewrite: durability claim → pop/feel ("Velocity Hybrid Core, AeroGrade Carbon Fiber Face… the liveliest paddle…"). Prices → gate #2. Trust badge #2 (Lifetime Warranty) → Flamingo warranty. Micro-trust: drop "Backed for life." |
| 1 | Hero promise (lower-left) | **REWRITE** | Peacock promise is about playing the same at month six (durability). Flamingo → pop/feel benefit. |
| 2 | **CONSTRUCTION** | **SWAP + light REWRITE** | Body is shared platform (carbon, roughness, dual-stamp) — keep. Swap the core sentence (Atomic Foam Core → Velocity Hybrid Core) and **drop the "lifetime warranty on the construction" line**. |
| 3 | **PROS** (2×2 grid) | **SWAP photos + copy** | Pros → Genie / Augie Ge / Jalina Ingram (+4th, gate #3). Lede: drop "Backed for Life" from the construction list. |
| 4 | **AEROGRADE + feature rows** | mixed | Intro: KEEP AeroGrade Construction™ definition (carbon, roughness) — **rewrite the core sentence** (Atomic Foam Core → Velocity Hybrid Core: foam + honeycomb, pop/feel). **Row 1** Atomic Foam Core → **Velocity Hybrid Core** (REWRITE). **Row 2** Carbon Face — **KEEP**. **Row 3** Dual-Stamp — **KEEP**. **Row 4** Lifetime Warranty → **REWRITE/replace** (Flamingo warranty, or swap for a Velocity-Core/pop benefit — gate #1, #6). |
| 5 | **FOUNDER** (Charles Darling) | **KEEP + light REWRITE** | Same photo/caption. Body mostly shared; drop/adjust the "lifetime warranty… defensible" clause. |
| 6 | **COUNTER "What If It's Your Paddle?"** | **REWRITE or DROP** | Durability/degradation argument — doesn't fit Flamingo. Gate #6. |
| 7 | **CERTIFICATIONS** badges | **REWRITE one** | UPA / USA / 30-Day = KEEP. "Lifetime Warranty on Construction" badge → Flamingo warranty. |
| 8 | **CONFIGURE** (shape/thickness selector) | **SWAP** | Mechanics + shape/thickness descriptions = KEEP (shared). Swap prices (gate #2), images → Flamingo renders, CTA "Peacock"→"Flamingo". |
| 9 | **FAQ** | mixed | #1 (tournament-legal) KEEP+swap; **#2 warranty → REWRITE** (gate #1); #3 (roughness) KEEP; #4 (shape) KEEP; #5 (thickness) KEEP — consider adding a **"Atomic vs Velocity core — which paddle?"** FAQ. (Peacock FAQ #6 Tour credit already removed.) |
| 10 | **CLOSE** | **REWRITE** | Anchor: "The Atomic Foam Core paddle. Optimized Spin. Backed for life." → "The Velocity Core paddle. Optimized Spin. [anchor]." CTA "Peacock"→"Flamingo"; drop "Backed for Life". Micro-trust: drop lifetime. |
| 11 | **FOOTER** | **SWAP + light REWRITE** | "Powered by Proton." KEEP. Blurb: drop "backed for life." Shop/Story/Support/Legal KEEP. Bar: drop "lifetime warranty on construction." |
| — | Mobile sticky CTA | **SWAP** | "Add Flamingo to Cart" (drop "Backed for Life"). |
| — | Dynamic JS (price/variant) | **SWAP** | Prices (gate #2), image filenames assets/flamingo/, "Peacock"→"Flamingo" in CTA template. |

---

## 6 · Copy / vocabulary deltas

**Replace:**
- "Atomic Foam Core" / "High-Density Atomic Foam Core" → **"Velocity Core" / "Velocity Hybrid Core"**
- Core description (durability) → **"a foam-and-honeycomb hybrid — solid foam for power, polypropylene honeycomb for springy pop; built for pop and feel; the liveliest paddle in the lineup."**
- "Project Peacock" → "Project Flamingo"; "Add Peacock to Cart" → "Add Flamingo to Cart"

**Drop entirely (durability/warranty):** "Backed for Life", "Lifetime Warranty on Construction", "for as long as the original owner plays", "most durable high-performance paddle", "plays the same at month six". Replace with Flamingo warranty (gate #1) + pop/feel language.

**KEEP (shared platform vocabulary):** "AeroGrade Construction™" (™ first mention only), "aerospace grade carbon fiber" (always full phrase), "roughness enhanced" / "structurally integrated", "dual-stamp UPA + USA Pickleball", "pushing the legal max", shape/thickness descriptions, "Charles Darling — Aerospace Executive, Proton Sports Founder".

**Still FORBIDDEN (carry over the bans):** "painted on" / "applied on top" / "coated"; the "Engineered in. Not painted on." anchor; "AeroWeave" (old name — use AeroGrade); "during the cure phase" (we removed it from Peacock); "last paddle you'll ever own" / "never decays".

**Hero H1 candidate:** `Aerospace Technology. Velocity Core. Optimized Spin. Built for Pop.` (gradient on "Velocity Core. Optimized Spin.") — confirm anchor at gate #8.

---

## 7 · Image map (9 product images + logos + people)

All 9 are deterministic Pillow composites (compose scripts in the proton-sports folder). Re-run each pointing at a **Flamingo Pink** source render, with Flamingo text + the pink `CYAN` constant. **Font sizes are already mobile-tuned** (we just bumped them) — don't change those. Output square PNGs → copy into `assets/flamingo/` with the short names (`01-aerograde.png` … `09-15mm.png`).

| Repo name | Compose script | Flamingo source | Text change | Notes |
|---|---|---|---|---|
| 01-aerograde | `compose_aerograde_square.py` | a Flamingo Pink finished face | callouts: "Atomic Foam Core"→"Velocity Hybrid Core"; subtitle drop "SCIENCE/BACKED FOR LIFE" → e.g. "BUILT FOR POP & FEEL." | overview w/ 5 callouts |
| 02-foam-core → **velocity-core** | `compose_core_split_v3.py` | **needs Velocity Core-only render** (gate #4) | title "VELOCITY HYBRID CORE"; sub "FOAM + HONEYCOMB. BUILT FOR POP & FEEL."; callouts: edge guard / honeycomb / foam / handle | split cutaway reveal |
| 03-carbon-face | `compose_aerospace_face.py` | Flamingo Pink face + macro | **KEEP** ("AEROSPACE GRADE CARBON FIBER FACE / ROUGHNESS ENHANCED. OPTIMIZED SPIN.") | shared platform |
| 04-dual-stamp | `compose_dual_stamp.py` | Flamingo Pink face | **KEEP** | shared platform |
| 05-warranty | `compose_lifetime_warranty.py` | Flamingo Pink face | **REWORK** (gate #1) — Flamingo warranty, or replace this slot with a Velocity/pop benefit image | biggest content change |
| 06-elongated | `compose_variants.py` cutout() | Flamingo Pink elongated | **KEEP** shape copy | |
| 07-wide-body | `compose_variants.py` cutout() | Flamingo Pink wide-body | **KEEP** shape copy | |
| 08-13mm | `compose_variants.py` fullbleed() | Flamingo 13mm edge | **KEEP** thickness copy | |
| 09-15mm | `compose_variants.py` fullbleed() | Flamingo 15mm edge | **KEEP** thickness copy | |

**Logos:** `assets/brand/proton-atom.png` + `proton-wordmark.png` — **reuse as-is** (brand-level). Favicon same.
**Pros photos:** `~/Downloads/2025_10 Proton Paddle Photos/Flamingo Elongated 15mm Pink/` has `flamingo-genie-bouchard-0{1,2}.png`, `flamingo-augie-ge-0{2,3}.png`, `flamingo-jalina-ingram-0{1,2}.png`. Crop to 4:5 like the Peacock pros.
**Founder:** reuse `charles-darling.jpg`.
**Construction photo** (§2): reuse Peacock `people/construction.png` or a Flamingo equivalent if Mike wants colorway match.

**Flamingo source render locations:**
- New square 15mm set: `proton-sports/source-photos/series-three-project-flamingo-square-15mm-new/` (Pink + Blue, incl. `07-Flamingo-Tech-Specs-15mm-Square-Pink.png`).
- Main set: `proton-sports/source-photos/series-three-project-flamingo/`.
- Full photo library (all shapes/thicknesses, Pink + Blue, pros, tech-specs, features-benefits): `~/Downloads/2025_10 Proton Paddle Photos/Flamingo *`.
- Old/earlier Flamingo composites (reference only, outdated naming): `proton-sports/output/series-three-project-flamingo-square-15mm-new/`.

---

## 8 · Build sequence (tomorrow)

1. **Scaffold** the Flamingo repo (§3); rename `assets/peacock`→`assets/flamingo`; update image paths in `index.html`.
2. **Recolor**: swap the 4 CSS accent vars → flamingo pink (§4); rename `--peacock`→`--flamingo`.
3. **Copy swap**: find/replace SKU identity + core name + CTAs + breadcrumb + alt text (§6).
4. **Rewrite** the durability/warranty parts: hero H1/deck/promise, construction core line, feature row 1 (Velocity Core) + row 4 (warranty), founder clause, §6 counter, certs badge, FAQ #2, close, footer, badges, sticky (§5) — using confirmed answers to gates #1, #6, #8.
5. **Images**: set `CYAN` → pink in the compose scripts; re-run each with Flamingo Pink sources + Flamingo text (§7); copy 9 PNGs into `assets/flamingo/`. Handle the Velocity Core split (gate #4).
6. **Pros**: crop + drop in the 4 Flamingo pro photos; update names/roles.
7. **Verify** desktop + mobile via headless Chrome (nav logo, pros 2×2 / mobile 1-up full-width, feature text-above-image on mobile, image text legible, no "Backed for Life"/lifetime leftovers, accent fully pink). Grep the final HTML for "peacock", "atomic", "lifetime", "backed for life" to catch stragglers.
8. **Commit + push** → enable/confirm GitHub Pages → hard-refresh to check.

---

## 9 · Quick file inventory

- **Peacock template:** `~/code/proton-peacock-pdp-preview/index.html` + `assets/{brand,peacock,email}/`
- **Compose scripts:** `proton-sports/{compose_aerograde_square,compose_aerospace_face,compose_dual_stamp,compose_lifetime_warranty,compose_variants,compose_core_split_v3,compose_build_overview,mask_utils}.py` + `.venv` (Pillow + scipy)
- **Copy doc (Peacock As-Built + Appendix A Flamingo crossover guide):** `~/Downloads/Proton Peacock PDP — Final Copy (As Built) 2026-05-29.md`
- **Messaging System v2 (Velocity Core, lineup, mechanism table):** `~/Downloads/2026-05-25-Proton-Messaging-System-CLIENT-REVIEW-v2.md`
- **Flamingo renders:** see §7.

---

### One-line summary
Same template + pink accent + Flamingo identity + Velocity (foam+honeycomb) Core + pop/feel story, **minus** lifetime warranty / "Backed for Life." The construction platform (AeroGrade, carbon, roughness, dual-stamp, shapes, thickness, founder) is shared verbatim. Confirm the 8 gates (warranty term, prices, pros, Velocity Core render, accent, counter, Tour FAQ, hero anchor) and the rest is mechanical.
