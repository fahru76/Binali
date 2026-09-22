# Binali Frontend Design Contract

## Research Log
- Existing `index.html` and `assets/` inspected before redesign; preserved verified content, interactions, credentials, WhatsApp flows, gallery, lightbox, and social embeds.
- User selected the primary direction: bold high-visibility construction-site signage on a dark ground, with rich motion.
- Local `omh design data` query was attempted but unavailable in this environment; tokens below are explicit product decisions, not framework defaults.

## Atmosphere & Identity
- Primary taste direction: **Minimalist / editorial**, adapted for a modern residential contractor.
- Adjectives: clear, trustworthy, human.
- Signature element: an obvious service-path selector that lets a visitor choose build, renovation, materials, or labour without deciphering marketing copy.
- Rejected prior direction: high-visibility construction signage. It was visually loud but reduced readability and made the page feel like a campaign poster instead of a helpful contractor guide.
- Audience: Terengganu homeowners and landowners evaluating a house build, renovation, materials, or construction labour.
- Goal: establish credibility quickly, show real work, and drive a qualified WhatsApp enquiry.
- Anti-slop decisions: no gradients as decoration, no rounded card system, no generic icon-card grid, no glass surfaces, no serif/editorial default, no placeholder copy.

## Color
- `--charcoal: #17233D` — deep navy surface and primary text on light ground.
- `--ivory: #F8FAFC` — cool white reading surface.
- `--accent: #2F6FED` — primary action and focus signal.
- `--line: #D9E2EF` — soft blue-grey borders and structural rules.
- `#F5F7FB` — text on dark surface.
- `#BEC9D8` / `#8D9BB0` — secondary dark-surface text.
- Proportion: approximately 70% cool-white reading ground / 25% navy / 5% blue signal, varying by section rhythm.
- Contrast floor: WCAG AA minimum; never use yellow as small body text on light ground.

## Typography
- Display/body: `DM Sans`, fallback Arial, sans-serif; 400/500/600/700 with sentence case.
- Utility/data: `DM Mono`, monospace; uppercase, 11px, tracked.
- Body minimum: 16px with 1.6 line-height for comfortable reading.
- Display scale: 3rem mobile hero, 2.25–4rem section headings, up to 6rem desktop hero.
- Display line-height: 1.02–1.08; avoid condensed text for paragraphs and controls.
- No CJK-specific surface requirement; if added, keep fallback coverage and minimum 14px body size.

## Spacing & Layout
- Existing Tailwind spacing scale remains the layout authority; major sections use 5/6/7/8/12/14/20/24/32 rhythm.
- Container: existing `max-w-7xl`, with 20px mobile and 32px desktop gutters.
- Grid: asymmetric editorial/construction layouts where hierarchy matters; 2-column project choices; 4-column scope at large widths; gallery 2→4 columns.
- Mobile breakpoint: 640px visual adjustments; existing responsive classes govern 768px and 1024px transitions.
- Scroll owner: document body; `overflow-x:hidden` prevents horizontal bleed.

## Components
- **Header:** fixed, transparent over hero, dark scrolled state; default/hover/focus-visible/active navigation states. CTA uses yellow signal.
- **Primary CTA:** yellow rectangle, zero radius, hard offset shadow; hover translates -2px with larger shadow; keyboard focus must remain visible.
- **Secondary CTA:** transparent border, light/dark contextual text; hover fills with a low-opacity surface.
- **Photo card:** square/rectangular hard border, image zoom and contrast/saturation hover; keyboard activation through native anchor/button.
- **Gallery filter:** native button; default outlined, active charcoal/yellow-context, focus-visible required; filter empty state is not applicable because both categories have real assets.
- **Lightbox:** modal with protected visual focus, close button, Escape, arrows, touch swipe; open/closed states; image load failure should not block close.
- **Quote form:** native labels/inputs/select/textarea; 3-step progression; default, focus-visible, invalid/error, success, and persisted draft states. Disabled/loading are not currently implemented and remain accepted debt.
- **Social embeds:** lazy loading placeholders for TikTok/Facebook; fallback links remain visible if third-party scripts are blocked.
- **Mobile action bar:** fixed Call/WhatsApp/Quote actions; stable height and high contrast.

## Motion & Interaction
- Reveal motion: translateY 28px + opacity, 650ms ease; only `.reveal` elements animate.
- Photo hover: 700ms image transform and 400ms filter transition.
- CTA hover: 200ms transform/shadow transition.
- Scroll progress and sticky header update on scroll.
- Lightbox transitions use state change; touch swipe and keyboard arrows are supported.
- `prefers-reduced-motion: reduce` disables reveal and image/CTA transitions and disables smooth scrolling.
- No scroll library; native scroll, anchors, IntersectionObserver, and touch events are used.

## Depth & Surface
- No blur/glass system.
- Primary depth is hard 4px/7px CTA shadow; photo borders and structural rules provide separation.
- Cards and controls use 8–12px radius to signal approachability without becoming soft or toy-like.

## Accessibility Constraints & Accepted Debt
- Preserve semantic headings, native links/buttons, labels, form controls, alt text, dialog attributes, Escape close, and keyboard gallery navigation.
- Maintain visible focus through native outline plus accent border/shadow; future visual edits must not remove it.
- Existing third-party embeds may fail under blockers; visible fallback links are intentional.
- Accepted debt: CTA/form loading disabled state is not implemented; static navigation has no current-section indicator; Pages deploy remains CDN-dependent for Tailwind.
- Performance budget: target LCP <2.5s (published good threshold) on a cold first visit at 390px viewport, mid-tier mobile, 4G; baseline is **not observed in this run**. LCP attribution to be captured before optimization; likely hero image/font load.
- Visual QA status: implementation and live-page marker verification observed; rendered screenshot loop at 1440/768/375 is still required before visual PASS.
