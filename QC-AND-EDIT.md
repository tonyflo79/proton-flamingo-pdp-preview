# Flamingo PDP — QC & Edit Guide (build day)

**Repo:** `~/code/proton-flamingo-pdp-preview` · **Live:** https://tonyflo79.github.io/proton-flamingo-pdp-preview/
**Companion:** `BUILD-HANDOFF.md` (full section/image map). This doc = the tactical fill-in-the-blanks + QC pass.

**How to work:** edit `index.html`; every edit spot is tagged — search the file for **`FLAMINGO TODO`** (7 markers). Preview by opening `index.html` in a browser. When done, run STEP 4 QC, then STEP 5 deploy.

---

## STEP 1 — Confirm gates with Mike (fill these in first)

```
1. Warranty term (NOT lifetime):  ______________________________
2. Prices: Elongated $______  Wide-Body $______   prior retail $______
3. Pros (4): Genie Bouchard, Augie Ge, Jalina Ingram, + ______________
4. Velocity Core "core-only" render path: ______________________________
5. Accent pink OK? (candidate flamingo gradient already applied)  Y / N → tweak: ______
6. §6 Counter: [ ] rework to pop/feel   [ ] drop section
7. Tour-credit FAQ: keep removed?  Y / N
8. Hero anchor (replaces "Backed for Life"): ______________________________
   (candidates: "Built for Pop." / "The Liveliest Paddle." / "Pop & Feel.")
```

---

## STEP 2 — Copy edits (current → recommended). Fill `[BRACKETS]` from STEP 1.

**Hero H1** (gradient stays on the middle two lines)
`Aerospace Technology. Atomic Foam Core. Optimized Spin. Backed for Life.`
→ `Aerospace Technology. Velocity Core. Optimized Spin. [ANCHOR].`

**Hero deck**
`The High-Density Atomic Foam Core, AeroGrade Carbon Fiber Face and Lifetime Warranty on the Construction make this the most durable high-performance paddle in the industry.`
→ `The Velocity Hybrid Core and AeroGrade Carbon Fiber Face make this the liveliest high-performance paddle in the lineup — built for pop and feel without giving up power.`

**Hero promise** (desk + mobile copies — edit BOTH)
`The paddle that plays the same at month six… That's what AeroGrade construction gives you — leading to optimized power, spin, feel and control across the long lifetime of the paddle.`
→ `Pop the moment it touches the ball — and the feel to place it. That's what AeroGrade Construction with a Velocity Core gives you — a foam-and-honeycomb hybrid tuned for liveliness, optimized power, spin, feel and control.`

**Construction body** (§2)
`…An Atomic Foam Core at the heart of the paddle. With extra durability built into every layer. Backed by a lifetime warranty on the construction.`
→ `…A Velocity Hybrid Core at the heart of the paddle — solid foam for power, polypropylene honeycomb for springy pop. Built for liveliness and feel.`

**AeroGrade intro core sentence** (§4)
`…At the heart of the paddle sits the Atomic Foam Core — a precision-engineered, consistent foam core … The core is consistent because the foam is designed for performance and longevity.`
→ `…At the heart of the paddle sits the Velocity Hybrid Core — solid foam engineered together with a polypropylene honeycomb for springy, lively response. The face is rough because the carbon is rough. The core is fast because the honeycomb is built for pop.`

**Feature row 1** — heading + body
`High-Density Atomic Foam Core` / `A precision-engineered, consistent foam core … Built for extra durability and shot-to-shot consistency.`
→ `Velocity Hybrid Core` / `A foam-and-honeycomb hybrid at the heart of the paddle — solid foam for power, polypropylene honeycomb for springy responsiveness. Built for pop, feel, and a lively, fast face.`

**Feature row 4** — heading + body (GATE #1)
`Lifetime Warranty on Construction` / `Proton stands behind the build for as long as the original owner plays. Full coverage on the carbon surface and the Atomic Foam Core.`
→ **Option A (Flamingo warranty):** `[TERM] Warranty on Construction` / `Proton stands behind the build with a [TERM] warranty — coverage on the carbon surface and the Velocity Core.`
→ **Option B (replace slot w/ benefit):** `Built for Pop & Feel` / `The Velocity Hybrid Core delivers the liveliest, fastest face in the lineup — pop off the paddle without losing control.`

**Founder body clause** (§5) — drop the warranty tail
`…the foam tuned to a consistent density, and a lifetime warranty behind the build that has to be defensible because the engineering is real.`
→ `…and a Velocity Core tuned for pop and feel — engineering you can feel on every shot.`

**§6 Counter** (GATE #6) — durability arg doesn't fit Flamingo
→ **Rework:** headline `Want more pop — without losing control?`; body about the Velocity Core being lively *and* controllable; keep closing `Pushing paddle design to the legal max.` (drop the degradation/durability claim entirely). **Or** delete the whole `<section>`.

**Certifications badge** (§7) — 3rd badge
`Lifetime Warranty on Construction` → `[TERM] Warranty on Construction` (or swap for another cert).

**Configure** (§8) — prices (GATE #2): update chips, price-row, was-line, scard `$195/$175`, and **JS** `priceFor()` + default state. CTA already says "Add My Flamingo to Cart".

**FAQ #2** (GATE #1) — rewrite for the Flamingo warranty term. Consider adding a FAQ: **"Atomic vs Velocity Core — which paddle is for me?"** (Peacock = durability/lifetime; Flamingo = pop/feel/lively).

**Close anchor** (§10)
`The Atomic Foam Core paddle. Optimized Spin. Backed for life.`
→ `The Velocity Core paddle. Optimized Spin. [ANCHOR].`

**Trust badges / micro-trust / footer** — drop every "Backed for life" / "Lifetime warranty":
- Hero trust badge #2 → `[TERM] Warranty on Construction`; badge #4 prior-retail price → gate #2.
- Hero micro-trust + close micro-trust: `Backed for life.` → `Built for pop.` (or drop).
- Footer blurb: drop `backed for life.`; footer bar: drop `Lifetime warranty on construction`.
- Mobile sticky CTA: drop "Backed for Life".

---

## STEP 3 — Regenerate the 9 images (Flamingo Pink)

In `~/code/client-work/copywriting-business/clients/proton-sports/`. **First** set the accent in each compose script: `CYAN = (95,213,224)` → `CYAN = (255,111,165)`. Then run with Flamingo Pink sources (font sizes are already mobile-tuned — don't touch). Copy each output → `assets/flamingo/` with the short name.

| Image | Script | Source (Flamingo Pink) | Text |
|---|---|---|---|
| 01-aerograde | compose_aerograde_square.py | a clean Flamingo Pink face | callouts: core→"Velocity Hybrid Core"; subtitle drop "BACKED FOR LIFE" |
| 02-foam-core | compose_core_split_v3.py | **Velocity Core render (gate #4)** | title "VELOCITY HYBRID CORE" / "FOAM + HONEYCOMB. BUILT FOR POP & FEEL." |
| 03-carbon-face | compose_aerospace_face.py | Flamingo Pink face + macro | KEEP (shared) |
| 04-dual-stamp | compose_dual_stamp.py | Flamingo Pink face | KEEP (shared) |
| 05-warranty | compose_lifetime_warranty.py | Flamingo Pink face | REWORK (gate #1) or swap to a pop/feel image |
| 06-elongated / 07-wide-body | compose_variants.py | Flamingo Pink elong/wide | KEEP shape copy |
| 08-13mm / 09-15mm | compose_variants.py | Flamingo 13mm/15mm edge | KEEP thickness copy |

Sources: `proton-sports/source-photos/series-three-project-flamingo*` and `~/Downloads/2025_10 Proton Paddle Photos/Flamingo *`.
Pros photos: `~/Downloads/2025_10 Proton Paddle Photos/Flamingo Elongated 15mm Pink/flamingo-{genie-bouchard,augie-ge,jalina-ingram}-*.png` → crop 4:5 → `assets/flamingo/people/`. Founder `charles-darling.jpg` reused.

---

## STEP 4 — QC checklist

**Automated (run in repo):**
```bash
grep -i "peacock" index.html        # expect: only the scaffold-banner origin notes, nothing user-facing
grep -i "backed for life\|lifetime\|atomic foam\|most durable\|month six" index.html   # expect 0 (unless intentionally kept)
grep -nE "2CE5C7|5FD5E0|95,213,224|--peacock" index.html   # expect 0 (no teal leftovers)
grep -nE "\$280|\$195|\$175" index.html    # confirm prices match gate #2
grep -c "FLAMINGO TODO" index.html         # expect 0 when all rewrites done; remove the banner too
```
**Visual (headless desktop 1366 + mobile 414):**
- [ ] Nav: Proton atom logo upper-left; accent fully **pink** (no teal anywhere)
- [ ] Hero H1 = Velocity Core; no "Backed for Life"; prices correct
- [ ] All 9 product images are **Flamingo Pink** (not teal placeholders); image text legible on mobile
- [ ] Pros: 2×2 desktop / 1-up full-width mobile; correct Flamingo pros + names
- [ ] Mobile: feature headline/copy sits **above** the image
- [ ] Construction / Feature row 1 = Velocity Core (foam+honeycomb); row 4 + counter reworked per gates
- [ ] Footer / certs / micro-trust / sticky CTA: no lifetime/Backed-for-Life leftovers; "Flamingo" everywhere
- [ ] Remove the scaffold TODO banner + all `FLAMINGO TODO` comments

---

## STEP 5 — Deploy
```bash
cd ~/code/proton-flamingo-pdp-preview
git add -A && git commit -m "feat: Flamingo PDP copy + Flamingo images" && git push origin main
```
GitHub Pages auto-builds in ~30–90s → hard-refresh (Cmd+Shift+R) the live URL.
