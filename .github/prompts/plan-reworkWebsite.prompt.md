## Plan: Beamo Website Revision 1

Thirteen UI/UX changes across index.html, css/styles.css, and js/main.js. All are HTML/CSS/JS edits — no build tools needed.

**Steps**

1. **Reduce border radius** — In css/styles.css L27-28, reduce `--radius` from `12px` to `8px` and `--radius-lg` from `20px` to `14px`. These cascade to feature cards, form inputs, testimonial cards, contact form, and the code block.

2. **Emphasize hero mesh gradient** — In css/styles.css L253-262, bump the alpha values on the 5 `radial-gradient` layers in `.hero-mesh`. E.g. teal from `0.25` → `0.35`, lime from `0.2` → `0.3`, yellow from `0.15` → `0.22`, green from `0.18` → `0.26`, peach from `0.1` → `0.16`. This makes the mesh more visible without being overpowering.

3. **Glass-like blur on navbar** — The navbar (css/styles.css L148-157) already has `backdrop-filter: blur(20px)` and `rgba(255,255,255,0.85)`. Enhance the glass effect: lower background alpha to `rgba(255,255,255,0.55)`, add a subtle `border: 1px solid rgba(255,255,255,0.25)`, and add a soft `box-shadow: 0 4px 30px rgba(0,0,0,0.04)` so it feels more translucent/frosted even before scroll. Keep the `.scrolled` class for additional shadow.

4. **Replace nav logo to `assets/logo.svg`** — In index.html line 19, change `src="assets/beamo-submark.svg"` to `src="assets/logo.svg"`. The logo.svg is the full wordmark (4000×1250 viewBox), so also adjust `.logo-img` height in CSS if needed (keep `height: 36px; width: auto`).

5. **"Get Started" button: white text + mesh gradient background** — In css/styles.css L95-115, change `.btn-primary` to use a mesh gradient as the default background instead of solid teal: `background: linear-gradient(135deg, var(--primary), var(--secondary), var(--accent-green))`. Keep `color: white`. Remove or adjust the `::before` hover overlay since gradient is now the default — on hover, slightly shift the gradient (e.g. `background-position` shift or a subtle brightness/scale change). This affects the nav CTA (index.html line 33), hero CTA (line 44), "Book a Tour" (line 109), "Request a Consultation" (line 186), "Send Message" (line 406).

6. **Replace '01'/'02' labels with 'SERVICES'** — In index.html line 63, change `<span class="service-label">01</span>` to `<span class="service-label">SERVICES</span>`. In index.html line 149, change `<span class="service-label">02</span>` to `<span class="service-label">SERVICES</span>`.

7. **Update on-site amenities description** — In index.html line 106, replace the `<p>` text `"Coffee bar, meeting rooms, lounge areas, and event spaces — all included."` with `"Refreshments and other amenities to support your daily work needs."`.

8. **Add "High-Performance Desktop Computer" feature card** — In index.html after the On-Site Amenities card (closing `</div>` around line 107) and before the closing `</div>` of `.feature-grid`, add a new `.feature-card` with a monitor/desktop SVG icon (e.g. Feather `monitor` icon), heading `"High-Performance Desktop Computer"`, and description `"Boost productivity with a powerful desktop and dedicated graphics, ideal for demanding tasks."`. This brings the workspace grid to 6 cards (3×2 on desktop).

9. **Digital solution visual: Safari-like browser with typing animation** — This is the most complex change:
   - **HTML** (index.html L137-147): Replace the `.illus-code` block with a `.browser-frame` container comprising: a `.browser-toolbar` (3 traffic-light dots, a URL bar placeholder) and a `.browser-body` containing the code with line numbers. Each code line gets a `<span class="line-number">` (1, 2, 3) and the existing `<beamo>` markup.
   - **CSS** (css/styles.css L490-510): Style `.browser-frame` as a flat Safari-like window: `border-radius: var(--radius)`, glass-like border (`border: 1px solid rgba(255,255,255,0.3)`, `background: rgba(255,255,255,0.15)`, `backdrop-filter: blur(16px)`, subtle `box-shadow` like the attached image). Style `.browser-toolbar` with a light bar, 3 colored dots (red/yellow/green, 10px circles). Style `.browser-body` with dark or light code area. Add `.line-number` styling (muted color, right-aligned, fixed width). Replace `.illus-code` styles.
   - **CSS** (new keyframes): Add `@keyframes typeWriter` that animates `width` from 0 to 100% using `steps()` for each code line, with staggered `animation-delay`. Add `@keyframes blinkCursor` for a blinking cursor (`|`) at the end of the last typed line using `border-right` or `::after` pseudo-element toggling `opacity`.
   - **JS** (js/main.js): Add a typing animation function triggered by IntersectionObserver when the browser frame scrolls into view. Sequentially reveal each character of each line, then show a blinking cursor at the end. This gives a more realistic feel than pure CSS.

10. **Improve testimonials** — Multiple sub-changes:
    - **HTML** (index.html L264-300): Remove the 3 `<div class="testimonial-stars">★★★★★</div>` elements. Remove the 3 `<div class="testimonial-avatar">XX</div>` elements. Remove `<strong>` wrapping from names (Sara Mitchell, James Rodriguez, Aisha Lowe). Add a large open-quote SVG/character at the start of each `.testimonial-card` (before `blockquote`): `<div class="quote-icon">"</div>` or use an SVG open-quote icon.
    - **CSS** (css/styles.css L821-870): Remove `.testimonial-stars` styles. Remove `.testimonial-avatar` styles. Add `.quote-icon` styling: large decorative open-quote (font-size ~3rem, color `var(--primary)` at ~0.3 opacity, line-height 1). On `blockquote`, remove `font-style: italic`, increase `font-size` from `0.95rem` to `1.05rem` or `1.1rem`. On `.testimonial-author strong` (now just a plain span), remove `font-weight: 700` (don't bold the name).

11. **Accordion animation + single-open behavior** —
    - **CSS** (css/styles.css L882-940): Add smooth open/close animation to `.faq-answer`: use `max-height` transition (from `0` with `overflow: hidden` to a set max-height). Add `transition: max-height 0.35s ease` on `.faq-answer`. Style `.faq-item:not([open]) .faq-answer` with `max-height: 0; padding: 0; overflow: hidden`. Note: the native `<details>` element doesn't animate well, so we'll need to handle this with JS-controlled classes instead of relying on the `[open]` attribute for animation.
    - **JS** (js/main.js): Add accordion logic: query all `.faq-item` elements. On each `summary` click, prevent default toggle, close all other open items (remove `[open]` attribute with animation), then toggle the clicked one. Animate using `requestAnimationFrame` or `el.animate()` for smooth height transitions. Only one `<details>` can be `[open]` at a time.

12. **Add email, phone, address to contact section** — In index.html L370-380, after the `<p>` description and before `.social-links`, add a `.contact-details` list:
    - Email: `hello@beamo.co` (with envelope SVG icon)
    - Phone: `+1 (555) 123-4567` (with phone SVG icon)
    - Address: `123 Innovation Drive, Suite 400, San Francisco, CA 94105` (with map-pin SVG icon)

    Style `.contact-details` in CSS with flexbox column, icon + text rows, matching the existing section aesthetic.

13. **Footer: white background, remove logo, copyright left-aligned** —
    - **HTML** (index.html L399-410): Remove the `.footer-logo` div containing the submark image. Keep `<p class="footer-copy">` and `.footer-links`.
    - **CSS** (css/styles.css L955-990): Change `.footer` background from `#2d2d2d` to `var(--white)` or `#ffffff`. Update `color` from `rgba(255,255,255,0.6)` to `var(--text-light)`. Adjust `.footer-container` to `justify-content: flex-start` with copyright on the left and links on the right (use `margin-left: auto` on `.footer-links`). Add a subtle `border-top: 1px solid rgba(0,0,0,0.08)` for separation. Update `.footer-links a:hover` color to `var(--primary)` instead of white.

---

**Verification**
- Open `index.html` in a browser and visually inspect each section against the feedback list
- Test navbar glass effect by scrolling partially — should see page content blur through
- Check that "Get Started" buttons all show mesh gradient with white text
- Confirm only one FAQ accordion item opens at a time, with smooth animation
- Verify the Safari browser frame shows typing animation with blinking cursor when scrolled into view
- Test responsive breakpoints (1024px, 768px, 480px) — ensure new feature card, contact details, and browser frame adapt properly
- Confirm footer is white with copyright left-aligned and no logo

**Decisions**
- Border radius reduced to `8px`/`14px` (moderate reduction; not too sharp)
- Typing animation implemented in JS (not pure CSS) for realistic sequential character reveal
- FAQ accordion uses JS-controlled open/close to support animation + mutual exclusion (native `<details>` doesn't animate smoothly)
- Contact details use placeholder values (email, phone, address) — user can substitute real ones
- All `.btn-primary` instances get mesh gradient (consistent branding)
