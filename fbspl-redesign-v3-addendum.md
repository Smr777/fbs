# FBSPL Redesign — v3 Addendum (Header + Funnel now fully in scope, premium design system, full-funnel pass)

**This supersedes the exclusions in v2.** Header.tsx and ContactUs.tsx are no longer off-limits — run v2's Prompts A (color), B (hero bg), C (text pass) again but WITHOUT the "exclude Header.tsx / ContactUs.tsx" lines. Then run the new prompts below.

## Updated run order (full sequence, start to finish)

1. v1 Prompt 0 — structural refactor
2. v2 Prompt A — color pass, **now including Header.tsx and ContactUs.tsx**
3. v2 Prompt B — hero background
4. v2 Prompt C — BPO→consultancy text pass, **now including ContactUs.tsx's "Insurance Outsourcing" dropdown option**
5. v1 Prompts 3–9, 12 — stats band, marquee, services grid, value props, insights row, tech spotlight, testimonials, footer
6. **New Prompt E** — full Header redesign
7. **New Prompt F** — full funnel/ContactUs redesign
8. **New Prompt G** — premium AI-corporate design system pass (whole site)
9. **New Prompt H** — full-page conversion funnel review
10. v2 Prompt D — final verification, **edit it first**: remove the two checks that say Header/ContactUs "should show no changes" — replace with "confirm Header and ContactUs reflect the new premium design and pass a manual click-through test"

---

## Prompt E — Full Header Redesign

```
Fully redesign src/components/Header.tsx to premium-corporate standard, using the reference site (https://www.fbspl.com) as the interaction/structure model, and our own brand palette (--color-brand-blue #001A7D, --color-persian-blue/--color-brand-cyan #002CCE, --color-carrot-orange #F29001) at full strength per the color pass already applied elsewhere.

1. Transparent-over-hero, solid-on-scroll behavior: header starts transparent with white logo/nav text over the dark hero, and transitions to a solid white (or --theme-brand-dark, your call — pick whichever reads more premium against our new hero) background with appropriately contrasting nav text once the user scrolls past the hero. Animate this transition smoothly (150-250ms), not an abrupt snap.
2. Mega-menu dropdowns (Services, Insights, About — using the existing toggleDropdown state) should feel premium: multi-column layout grouped by our real service/insight categories from src/data/websiteContent.ts, each item with its short description already in our data, generous padding, a subtle fade+slide-down entrance animation (framer-motion), and an accent-colored icon or bullet per category. Add a subtle divider or background-tint on the currently-hovered row within the dropdown.
3. Nav link hover states: underline-grow or color-shift to --color-carrot-orange, with a smooth transition — no instant color snaps anywhere in this component.
4. CTA button in the header (if one exists, e.g. "Book a Consultation" or similar — add one if it doesn't exist, since the reference always keeps a persistent header CTA) should be a solid --color-carrot-orange pill button, visible in both header states (transparent and scrolled).
5. Mobile menu: full-screen or slide-in drawer, dark background (--theme-brand-dark) with white text, categories as expandable accordions (not nested dropdowns — mobile needs tap-to-expand, not hover), smooth open/close animation, and a visible close (X) button.
6. Logo: keep our actual logo asset (src/Images/Logo.svg) — do not swap it for anything else, just make sure it renders correctly in both light and dark header states.

Preserve all underlying navigation/routing logic exactly as it currently works — this is a visual and interaction redesign only, not a routing change.
```

---

## Prompt F — Full Funnel / ContactUs Redesign

```
Fully redesign src/components/ContactUs.tsx (the final "business funnel" section of the page) as the site's premium hard-conversion moment, combining our existing content/logic with the reference site's visual treatment.

1. Background: full-width, --theme-brand-dark or a --color-brand-blue → --theme-brand-dark gradient, with the two existing blurred orb decorations (brand-cyan/10 and brand-blue/10 circles) intensified/repositioned so they still read as premium ambient depth rather than flat color — consider increasing their size/blur and adding a subtle slow drift animation via framer-motion.
2. Left column (pitch text + InteractiveEarth): keep the existing "Consultation & Strategy" eyebrow tag, headline, and description, but restyle for the dark background — white headline, light-gray/--text-on-dark-muted-equivalent body text, and re-theme the eyebrow tag and pulsing dot to use --color-carrot-orange instead of the current persian-blue/orange mix, for one consistent accent color throughout this section. Keep InteractiveEarth.tsx completely functionally intact — only wrap/reposition if needed for the new layout, do not alter its internal 3D logic.
3. Right column (form card): make this a bright white card floating on the dark background with real elevation (shadow-2xl or stronger, rounded-2xl or larger radius) — this contrast is the premium "spotlight" moment the reference site uses. Keep all current fields and validation logic (name, email, company, service, phone, country, state, source, requirement, opt-in) exactly as functionally implemented. Visually upgrade: better label/input spacing, floating or animated labels if feasible, clear focus states in --color-persian-blue, and inline success/error states using the existing AnimatePresence submitted/error logic — just give the success state (submitted === true) a more premium moment (a bigger checkmark animation, a warmer confirmation message) rather than a plain state swap.
4. Submit button: solid --color-carrot-orange, full width or prominent width, with a hover/press micro-interaction (scale or shadow lift), and a loading-spinner state while isSubmitting is true (check if one already exists — upgrade its visual polish if so, add one if not).
5. Do NOT change the "Insurance Outsourcing" dropdown option's label here independently of Prompt C's global rename — if Prompt C has already been re-run including this file, this option should already read whatever consultancy-oriented label you chose elsewhere; just confirm it's consistent, don't introduce a second variant.
6. Keep the certifying footnote line (ISO 27001/9001 mention) — restyle for dark background only.

This section should now feel like the single most premium, highest-contrast moment on the page — the payoff after everything the user scrolled through above it.
```

---

## Prompt G — Premium AI-Corporate Design System Pass

```
Do a cross-cutting design-system consistency pass across every section component in src/components/sections/, plus Header.tsx, Footer.tsx, ContactUs.tsx, and Testimonials.tsx. The goal: this should read as one cohesive premium AI-corporate product, not a set of independently redesigned sections. Specifically:

1. Typography scale: audit heading sizes (h2/h3 equivalents) across all sections and make sure there's a consistent scale (e.g. section headlines all use the same font-size/weight/tracking combination, eyebrow labels are all styled identically — same uppercase/tracking-widest/text-xs/font-bold treatment site-wide, not slightly different per section).
2. Spacing rhythm: normalize vertical section padding (py-* values) to a consistent set (e.g. all major sections use py-20 or py-24, not a mix of py-[64px], py-[62px], py-24 inconsistently) so the page has a predictable, premium vertical rhythm when scrolling.
3. Elevation/shadow system: define a consistent shadow scale (subtle card shadow, medium hover shadow, strong floating-card shadow like the new ContactUs form card) and apply the same shadow tokens across all cards site-wide (service cards, testimonial card, value-prop panels, footer newsletter box if any) instead of ad-hoc shadow values per component.
4. Micro-interactions: every interactive element (card, button, nav link, dropdown item) should have a consistent hover/press treatment — pick one primary hover pattern (e.g. subtle lift + shadow increase for cards, color-shift + underline for links, scale-down on press for buttons) and apply it uniformly rather than mixing different hover styles per section.
5. Scroll-reveal: audit which sections currently have entrance animations (fade/slide-in on scroll into view) vs which don't, and add consistent scroll-reveal treatment to any section currently missing it, using the same easing/duration values already established elsewhere in the codebase (check existing framer-motion transition configs for the values already in use, standardize on one set).
6. AI-forward visual accents: since this is positioned as an "AI-integrated" consultancy, make sure at least the Hero, TechSpotlight, and Services sections carry a consistent subtle "AI" visual motif (e.g. the existing grid-pattern/circuit-ring elements from Hero, or a subtle animated dot/node network pattern) rather than that motif appearing once and nowhere else — reuse the same visual language in 2-3 well-chosen spots rather than confining it to the hero alone.

List every inconsistency you find before fixing it, then apply the fixes.
```

---

## Prompt H — Full-Page Conversion Funnel Review

```
Review the entire homepage as a conversion funnel, in the order the sections currently render (confirm the current order first and list it back to me), and adjust copy/CTA placement — not full redesigns — so each section does its job in the funnel:

1. Hero: single clear primary CTA (e.g. "Book a Consultation") should be the most visually dominant action — confirm no competing secondary CTA is fighting for attention at this stage.
2. Trust/stats band: no CTA needed here — this section's only job is credibility. Confirm it doesn't awkwardly repeat the hero's CTA.
3. Services grid: each service card's "Learn More" link should feel like a natural next step for a specific visitor intent (an insurance-focused visitor clicks into insurance) — confirm every service card actually has a working, clearly visible CTA link.
4. Value props / Why Choose Us: this section should reinforce differentiation right after services, before asking for anything — confirm its own CTA ("Explore What Defines Us" or equivalent) doesn't compete with driving the user toward the main contact funnel, and either links to a relevant deeper page or is de-emphasized in favor of the eventual main CTA.
5. Client marquee + Testimonials: pure social proof, no CTA needed — confirm neither section has been accidentally given a heavy CTA that dilutes the funnel's focus.
6. Tech/Innovation spotlight: this is a secondary interest-capture moment — confirm its CTAs point to real internal pages (per Prompt 8 in v1) and are visually secondary to the final conversion section, not competing with it.
7. Insights row: soft-conversion, thought-leadership — confirm this doesn't out-compete the final CTA for visual weight; it should read as "explore more" not "convert now."
8. Final CTA / ContactUs funnel section: this must be the single most visually dominant CTA moment on the entire page (per Prompt F). Confirm no earlier section is inadvertently more visually striking than this one — if the new Hero or TechSpotlight redesigns from earlier prompts are competing with this section for "boldest moment on the page," dial one of them back slightly so the final contact section remains the clear peak.

Report the funnel order back to me with a one-line note per section on its funnel role, and flag (don't yet fix, just flag) anywhere you think the current design or copy undercuts that role, so we can decide together whether to adjust.
```

---

## Note on Prompt D (verification, from v2)

Update it: remove these two lines —
```
1. Run `git diff --stat src/components/Header.tsx` ... should show NO changes
2. Same check for src/components/ContactUs.tsx — should show no changes at all
```
Replace with:
```
1. Confirm Header.tsx now reflects the premium mega-menu redesign from Prompt E and all navigation/routing still functions correctly.
2. Confirm ContactUs.tsx now reflects the premium dark-funnel redesign from Prompt F, all form fields still validate/submit correctly, and InteractiveEarth still renders and rotates as before.
```
Keep the rest of Prompt D (tsc check, full visual dev-server pass) as-is.
