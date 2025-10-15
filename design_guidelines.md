# Credit Card Statement Parser - Design Guidelines

## Design Approach: Financial Data Platform

**Selected Approach**: Design System (Material Design) + Fintech Best Practices

Drawing from financial platforms like Plaid, Stripe, and modern banking dashboards, this application prioritizes trust, clarity, and efficient data handling. The design emphasizes security, professional aesthetics, and seamless data workflows.

---

## Core Design Elements

### A. Color Palette

**Dark Mode (Primary)**
- Background: `222 15% 8%` (deep charcoal)
- Surface: `222 15% 12%` (elevated cards)
- Primary: `217 91% 60%` (trust blue - financial institutions)
- Success: `142 76% 36%` (data confirmation)
- Warning: `38 92% 50%` (alerts, due dates)
- Text Primary: `210 20% 98%`
- Text Secondary: `215 20% 65%`
- Border: `217 20% 20%`

**Light Mode**
- Background: `0 0% 100%`
- Surface: `210 20% 98%`
- Primary: `217 91% 60%`
- Text Primary: `222 47% 11%`
- Border: `214 32% 91%`

**Accent Colors** (minimal use)
- Card Issuer Indicators: Subtle brand colors (Chase blue, Amex blue, Citi red tints)

### B. Typography

**Fonts**
- Primary: Inter (modern, professional fintech standard)
- Monospace: JetBrains Mono (for card numbers, amounts, data tables)

**Hierarchy**
- H1: 3xl/4xl, semibold (page titles)
- H2: 2xl, semibold (section headers)
- H3: xl, medium (card headers, data categories)
- Body: base, regular (descriptions, helper text)
- Data: sm/base, monospace (financial figures, card numbers)
- Labels: xs/sm, medium uppercase tracking-wide (form labels, status)

### C. Layout System

**Spacing Primitives**: Tailwind units of 2, 4, 6, 8, 12, 16
- Component padding: p-6 to p-8
- Section spacing: mb-8 to mb-12
- Card gaps: gap-6
- Form fields: mb-4 to mb-6

**Grid Structure**
- Main container: max-w-7xl mx-auto
- Upload area: max-w-2xl centered
- Results: Two-column on desktop (metadata + transactions), single column mobile

### D. Component Library

**Upload Zone**
- Large drag-and-drop area (min-h-64)
- Dashed border (border-2 border-dashed)
- PDF icon (central, 4xl size)
- Primary CTA button + secondary "browse files" link
- Supported formats badge
- Hover state: subtle background shift, border color intensify

**Data Display Cards**
- Frosted glass effect on dark mode (bg-opacity-10, backdrop-blur-sm)
- Rounded corners (rounded-xl)
- Subtle shadow on light mode
- Card issuer logo (top-right, subtle)
- Key-value pairs with clear visual separation

**Transaction Table**
- Sticky header on scroll
- Alternating row backgrounds (subtle zebra striping)
- Monospace for amounts (right-aligned)
- Date formatting consistent (MMM DD, YYYY)
- Category tags (rounded pills, muted colors)

**Status Indicators**
- Processing: Animated spinner + blue pulse
- Success: Green checkmark + fade-in animation
- Error: Red alert icon + shake animation (brief)
- File validation: Real-time feedback

**Action Buttons**
- Primary: Solid fill, semibold text, h-11
- Secondary: Outline variant on surfaces, ghost on images
- Download: Icon + label combo
- Clear/Reset: Ghost variant, subtle destructive color

### E. Key Interactions

**Upload Flow**
1. Drag-and-drop zone (idle state)
2. Drag-over highlight (border glow, background tint)
3. Upload progress (linear bar, percentage)
4. Parsing animation (skeleton loaders for data cards)
5. Results fade-in (staggered reveal, 100ms delay between cards)

**Data Viewing**
- Expand/collapse transaction details
- Hover tooltips for truncated data
- Click-to-copy for card numbers (with success toast)
- Filter/search transactions (if applicable)

**Download Options**
- Format selector (JSON/CSV toggle)
- Download button with icon
- Success confirmation toast

### F. Page Structure

**Header**
- App logo/title (left)
- Theme toggle (top-right)
- Minimal, clean navigation if multi-page

**Main Upload View**
- Centered upload zone
- Supported issuers display (5 logos in row, grayscale with color on hover)
- Sample data points list (what will be extracted)
- Security badge/trust indicator

**Results View**
- Summary card (top): Total balance, due date, billing cycle
- Card details card: Last 4 digits, issuer, card type
- Transaction table (main content, scrollable)
- Download section (sticky bottom or top-right)

**No Animation Philosophy**: Static, instant transitions. Focus on data clarity over decorative motion.

---

## Images

**Hero Section**: No traditional hero. Replace with functional upload zone featuring:
- Light, abstract financial pattern background (subtle, non-distracting)
- Or solid gradient: from primary color to darker shade
- Credit card iconography (outline style, not photo-realistic)

**Card Issuer Logos**: Use official SVG logos in grayscale (inactive), full color when active/selected

**Icons**: Material Icons (via CDN) for upload, download, security, check/error states

---

## Key Principles

1. **Trust First**: Professional, secure aesthetic. No playful elements.
2. **Data Clarity**: Monospace for financial data, clear hierarchy, ample whitespace
3. **Efficient Workflow**: Minimal steps from upload to results
4. **Responsive Tables**: Card-based layout on mobile, full table on desktop
5. **Accessibility**: WCAG AA contrast, keyboard navigation, screen reader labels