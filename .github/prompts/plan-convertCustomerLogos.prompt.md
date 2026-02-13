# Plan: Convert Customer Logos to Image Elements

Replacing text-based company names with actual logo images from `assets/customer/` and applying neutral gray styling. Using the 4 existing logo files (remotask, scale, toyota SVGs + sepi PNG), each duplicated 3 times for smooth infinite carousel scrolling.

## Steps

### 1. Update HTML logo structure
**File:** [index.html](index.html#L260-L275)

- Replace each `<div class="logo-item"><span>...</span></div>` with `<div class="logo-item"><img src="assets/customer/..." alt="..." /></div>`
- Use 4 logos: `customer-remotask.svg`, `customer-scale.svg`, `customer-toyota.svg`, `customer-sepi.png`
- Duplicate each logo 3 times (12 total items) to maintain smooth infinite scroll effect
- Add descriptive alt text for each logo

### 2. Update CSS styling
**File:** [css/styles.css](css/styles.css#L920-L938)

- Change `.logo-item span` selector to `.logo-item img`
- Remove text-specific properties: `font-size`, `font-weight`, `letter-spacing`, `white-space`
- Add image properties: `height: 40px` (or appropriate size), `width: auto`, `object-fit: contain`
- Apply grayscale filter: `filter: grayscale(100%) brightness(0.5) contrast(0.8)` to achieve #808080 neutral gray tone
- Update hover state: `filter: grayscale(0%) brightness(1) contrast(1)` to show original colors, or keep primary color overlay strategy
- Ensure smooth transition on hover

### 3. Adjust carousel spacing
**File:** [css/styles.css](css/styles.css#L917-L919)

- Review and potentially adjust `.logo-track` gap (currently `60px`) for better visual balance with images vs text
- Verify `.logo-item` padding (`20px 40px`) works well with image dimensions

## Verification

- Open index.html in browser
- Confirm all 4 company logos display as images (12 items total: 3 of each)
- Verify muted gray appearance (#808080 tone)
- Test hover effect shows logo colors or teal overlay
- Check infinite scroll animation runs smoothly without gaps
- Validate images are properly sized and aligned

## Decisions

- Using only 4 existing logo files from `assets/customer/` as confirmed
- Applied #808080 neutral gray via CSS filters for color consistency across SVG and PNG files
- Each logo duplicated 3 times (12 total) to maintain carousel density with fewer unique logos
