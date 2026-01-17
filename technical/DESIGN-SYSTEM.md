# 🎨 Design System & Brand Guidelines

## 1. Brand Identity

### Logo & Wordmark

```
Vera Logo:
├── Icon: Single leaf (represents growth, memories)
│   ├── Shape: Modern geometric leaf
│   ├── Colors: Gradient brand-primary to brand-accent
│   └── Usage: Icon-only for app, with wordmark for web
├── Wordmark: "Vera" serif typography
│   ├── Font: Playfair Display (logo only)
│   ├── Size: Minimum 40px height
│   └── Spacing: Keep 1.5x clear space around
└── Full Logo: Icon + Wordmark
    ├── Horizontal layout (preferred)
    ├── Vertical layout (app store)
    └── Minimum size: 80px width
```

### Brand Voice

```
Warm, Personal, Trustworthy
├── Warm: Like talking to a close friend
├── Personal: Acknowledging each family's unique story
├── Trustworthy: Professional, secure, reliable
└── Tone: Celebratory (milestones), reflective (memories)
```

---

## 2. Color Palette

### Primary Colors

```json
{
  "brand-primary": "#E85D75",
  "brand-primary-light": "#F5A4B8",
  "brand-primary-dark": "#C93860",
  
  "brand-accent": "#FFB347",
  "brand-accent-light": "#FFCF8F",
  "brand-accent-dark": "#FF9500",
  
  "brand-secondary": "#6B5B95",
  "brand-secondary-light": "#9D8BC7",
  "brand-secondary-dark": "#4A3F6B"
}
```

### Neutral Colors

```json
{
  "neutral-white": "#FFFFFF",
  "neutral-50": "#F9F9F9",
  "neutral-100": "#F3F3F3",
  "neutral-200": "#E8E8E8",
  "neutral-300": "#D1D1D1",
  "neutral-400": "#B0B0B0",
  "neutral-500": "#808080",
  "neutral-600": "#5A5A5A",
  "neutral-700": "#3A3A3A",
  "neutral-800": "#2A2A2A",
  "neutral-900": "#1A1A1A",
  "neutral-black": "#000000"
}
```

### Semantic Colors

```json
{
  "success": "#4CAF50",
  "success-light": "#A5D6A7",
  "success-dark": "#2E7D32",
  
  "warning": "#FF9800",
  "warning-light": "#FFE0B2",
  "warning-dark": "#E65100",
  
  "error": "#F44336",
  "error-light": "#EF9A9A",
  "error-dark": "#C62828",
  
  "info": "#2196F3",
  "info-light": "#BBDEFB",
  "info-dark": "#1565C0"
}
```

### Usage in UI

```
Backgrounds:
├── Primary background: neutral-white
├── Secondary background: neutral-50
├── Elevated (cards): neutral-white + shadow
└── Dark mode: neutral-900

Text:
├── Primary text: neutral-900
├── Secondary text: neutral-600
├── Disabled: neutral-400
└── Light (on brand): neutral-white

Accents:
├── Links: brand-primary
├── Hover: brand-primary-light
├── Active: brand-primary-dark
├── Milestones highlight: brand-accent
└── Interactive elements: brand-primary
```

---

## 3. Typography

### Font Family

```
Primary: "Inter" (system font stack fallback)
├── Weights: 400, 500, 600, 700
├── Used for: Body text, UI labels, buttons
└── File: System default (iOS SF Pro, Android Roboto)

Display: "Playfair Display" (headings only)
├── Weights: 700 (bold headings)
├── Used for: Page titles, album covers
└── Web only (not on mobile for performance)

Serif: "Crimson Text" (premium sections)
├── Weights: 400, 600
├── Used for: Story text on albums, special moments
└── Backup: Georgia (system serif)
```

### Type Scale

```
H1 - Display Large
├── Size: 32px (mobile), 48px (desktop)
├── Weight: 700
├── Line height: 1.2
├── Letter-spacing: -0.5px
└── Usage: Page titles, album covers

H2 - Display Medium
├── Size: 28px (mobile), 36px (desktop)
├── Weight: 700
├── Line height: 1.3
├── Usage: Section headings

H3 - Heading Large
├── Size: 24px
├── Weight: 600
├── Line height: 1.4
└── Usage: Card titles, subsections

H4 - Heading Medium
├── Size: 18px
├── Weight: 600
├── Line height: 1.5
└── Usage: Component headings

H5 - Heading Small
├── Size: 16px
├── Weight: 600
├── Line height: 1.5
└── Usage: Label headings

Body - Large
├── Size: 16px
├── Weight: 400
├── Line height: 1.6
└── Usage: Long-form content, descriptions

Body - Regular
├── Size: 14px
├── Weight: 400
├── Line height: 1.6
└── Usage: Body text, photo stories

Body - Small
├── Size: 12px
├── Weight: 400
├── Line height: 1.5
└── Usage: Captions, metadata

Caption
├── Size: 11px
├── Weight: 500
├── Color: neutral-600
└── Usage: Timestamp, age display, helper text

Button
├── Size: 14px
├── Weight: 600
├── Text-transform: Capitalize
└── Usage: All buttons
```

---

## 4. Spacing System

### Spacing Scale

```
xs:   4px
sm:   8px
md:  16px
lg:  24px
xl:  32px
2xl: 48px
3xl: 64px
4xl: 80px

Usage:
├── Component internal: xs, sm, md
├── Component spacing: md, lg
├── Section spacing: lg, xl
├── Page margins: xl, 2xl
└── Large sections: 2xl, 3xl
```

### Layout Spacing

```
Mobile (375px width):
├── Page margins: 16px (md)
├── Column gap: 16px
├── Row gap: 8px-16px
└── Card padding: 16px-24px

Tablet (768px width):
├── Page margins: 24px (lg)
├── Column gap: 24px
├── Max width: 600px (centered)
└── Card padding: 24px-32px

Desktop (1024px+):
├── Page margins: 40px
├── Column gap: 32px (2xl)
├── Max width: 1200px
└── Card padding: 32px (xl)
```

---

## 5. Sizing & Grid System

### Component Sizing

```
Heights:
├── Minimum touch target: 44px × 44px
├── Button height: 44px (mobile), 48px (desktop)
├── Input height: 44px
├── Card corner radius: 12px (iOS safe)
└── Icon size: 20px (buttons), 24px (nav)

Widths:
├── Full width: 100%
├── Sidebar: 280px (tablet/desktop only)
├── Card max width: 100%
├── Image aspect ratios:
│   ├── Profile photo: 1:1 (square)
│   ├── Timeline photos: 1:1 (square grid)
│   ├── Album cover: 3:4 (portrait)
│   └── Hero image: 16:9 (web only)
```

### Grid System

```
Mobile (4-column):
├── Column: 100% / 4 = 25%
├── Gutter: 8px
├── Margin: 16px
└── Breakpoint: max 375px

Tablet (6-column):
├── Column: 100% / 6 ≈ 16.67%
├── Gutter: 12px
├── Margin: 24px
└── Breakpoint: 376px - 768px

Desktop (12-column):
├── Column: 100% / 12 ≈ 8.33%
├── Gutter: 16px
├── Margin: 40px
├── Max width: 1200px
└── Breakpoint: 769px+
```

---

## 6. Elevation & Shadows

### Shadow System

```
Elevation 0 (None):
├── Usage: Flat backgrounds, no depth
└── Shadow: none

Elevation 1 (Subtle):
├── Shadow: 0 1px 2px rgba(0,0,0,0.05)
├── Usage: Dividers, separators
└── Border: 1px neutral-200

Elevation 2 (Card Base):
├── Shadow: 0 2px 8px rgba(0,0,0,0.08)
├── Usage: Cards, lifted panels
└── Border: none

Elevation 3 (Card Hover):
├── Shadow: 0 4px 12px rgba(0,0,0,0.12)
├── Usage: Card hover state
└── Transition: 200ms ease-out

Elevation 4 (Modal):
├── Shadow: 0 8px 24px rgba(0,0,0,0.15)
├── Usage: Modals, overlays
└── Backdrop: rgba(0,0,0,0.4)

Elevation 5 (Floating Action):
├── Shadow: 0 12px 32px rgba(0,0,0,0.2)
├── Usage: FAB, floating elements
└── Border: 2px brand-primary
```

### Corner Radius

```
Sizes:
├── xs: 4px (minimal rounding)
├── sm: 8px (inputs, small buttons)
├── md: 12px (standard, iOS safe)
├── lg: 16px (cards, modals)
└── full: 9999px (pill buttons, circles)

iOS Notch Safe Area:
├── Top padding: 44px
├── Bottom padding: 34px (home indicator)
├── Left/right: Dynamic (use safe area insets)
└── Card corners: Must respect safe area
```

---

## 7. Component Library

### Buttons

```
Primary Button
├── Background: brand-primary
├── Text: neutral-white
├── Padding: 12px 24px
├── Border radius: md (12px)
├── Height: 44px
├── Font: 14px weight 600
├── States:
│   ├── Default: brand-primary
│   ├── Hover: brand-primary-light
│   ├── Active: brand-primary-dark
│   ├── Disabled: neutral-300 + neutral-500 text
│   └── Loading: 50% opacity + spinner
└── Usage: Main CTAs (upload, save, checkout)

Secondary Button
├── Background: neutral-100
├── Text: brand-primary
├── Border: 1px brand-primary
├── Padding: 12px 24px
├── States:
│   ├── Hover: neutral-200
│   └── Active: neutral-300
└── Usage: Alternative actions (cancel, close)

Tertiary Button
├── Background: transparent
├── Text: brand-primary
├── Padding: 12px 24px
├── States:
│   └── Hover: neutral-50 background
└── Usage: Links, low-priority actions
```

### Input Fields

```
Text Input
├── Height: 44px
├── Padding: 12px 16px
├── Border: 1px neutral-300
├── Border radius: sm (8px)
├── Font: 14px weight 400
├── Placeholder: neutral-400
├── States:
│   ├── Focus: 2px solid brand-primary (outline)
│   ├── Error: 2px solid error
│   ├── Filled: neutral-900 text
│   └── Disabled: neutral-100 background
├── Helper text: 12px neutral-600
└── Error message: 12px error color

Label
├── Font: 14px weight 500
├── Color: neutral-900
├── Margin bottom: 8px (sm)
├── Required indicator: red asterisk
└── Usage: Above input fields
```

### Cards

```
Base Card
├── Background: neutral-white
├── Padding: 16px (md)
├── Border radius: lg (16px)
├── Border: 1px neutral-200
├── Shadow: elevation-2
├── Hover: elevation-3 (transition 200ms)
└── Usage: Photo containers, album previews

Photo Card
├── Aspect ratio: 1:1 (square)
├── Image: Contained (no crop)
├── Overlay:
│   ├── Hover: rgba(0,0,0,0.2) dark overlay
│   ├── Icons: Favorite, edit, delete (on hover)
│   └── Metadata: Age display (bottom-left)
├── Story text: 2-line truncate (below image)
└── Animation: Tap feedback (0.8 opacity, 95% scale)

Album Card
├── Aspect ratio: 3:4 (portrait)
├── Cover: Album design preview
├── Bottom section:
│   ├── Title: 16px weight 600
│   ├── Year: 14px neutral-600
│   └── Photo count: 12px neutral-500
└── CTA: "Customize" or "Order" button
```

### Navigation

```
Bottom Tab Navigation (Mobile)
├── Height: 60px (including safe area)
├── Background: neutral-white
├── Border-top: 1px neutral-200
├── Tabs: 4-5 items max
├── Tab items:
│   ├── Icon: 24px
│   ├── Label: 11px weight 500
│   ├── Active: brand-primary (icon + text)
│   ├── Inactive: neutral-600
│   └── Tap area: Full 60px height
└── Safe area: +15px bottom padding

Top Navigation (Desktop)
├── Height: 64px
├── Background: neutral-white
├── Shadow: elevation-1
├── Logo: 40px height
├── Menu items: Horizontal, 16px spacing
├── Right section:
│   ├── Search: Optional
│   ├── Notifications: Badge count
│   └── Profile dropdown: Avatar 36px circle
└── Mobile menu: Hamburger icon (24px)

Breadcrumb Navigation
├── Font: 12px weight 400
├── Color: neutral-600
├── Separator: " / " (neutral-400)
├── Last item: Bold (current page)
└── Usage: Desktop web only (Vera is mobile-primary)
```

### Modals & Overlays

```
Modal
├── Backdrop: rgba(0,0,0,0.4)
├── Animation: Fade in 200ms
├── Content box:
│   ├── Background: neutral-white
│   ├── Border radius: lg (16px)
│   ├── Shadow: elevation-4
│   ├── Max width: 90% (mobile), 500px (desktop)
│   ├── Padding: lg (24px)
│   └── Safe area: Respect notch + home indicator
├── Header:
│   ├── Title: H3 style
│   ├── Close button: 32px × 32px, top-right
│   └── Divider: 1px neutral-200
├── Content: Scrollable if height > 70vh
├── Footer:
│   ├── Divider: 1px neutral-200
│   ├── Buttons: Primary + Secondary (horizontal)
│   └── Padding: lg (24px)
└── Exit animation: Fade out 200ms

Dialog (Alert)
├── Content box: Max width 280px
├── Title: H4 style
├── Message: Body text
├── Buttons: 2 options (side-by-side or stacked)
└── Usage: Confirm actions (delete, discard)
```

### Notifications & Toast

```
Toast (Bottom message)
├── Position: Bottom-safe-area, 16px from bottom
├── Background: neutral-900
├── Text: neutral-white, 14px
├── Padding: 12px 16px
├── Border radius: md (12px)
├── Icon: 16px left side
├── Duration: 3-5 seconds
├── Animation: Slide up 300ms
└── Max width: 90% (mobile), 400px (web)

Notification Badge
├── Size: 20px × 20px (circle)
├── Background: error (red)
├── Text: neutral-white, 10px weight 700
├── Position: Top-right of icon
└── Usage: Unread count on notifications
```

---

## 8. Interaction & Animation

### Transitions

```
Fast (Short interactions):
├── Duration: 150ms
├── Easing: cubic-bezier(0.4, 0, 0.2, 1)
└── Usage: Button hover, icon changes

Standard (Medium interactions):
├── Duration: 300ms
├── Easing: cubic-bezier(0.4, 0, 0.2, 1)
└── Usage: Modal open/close, nav transitions

Slow (Long interactions):
├── Duration: 500ms
├── Easing: cubic-bezier(0.4, 0, 0.2, 1)
└── Usage: Page transitions, large animations
```

### Micro-interactions

```
Button Press
├── Visual: Scale 0.95, opacity 0.8
├── Duration: 100ms
├── Feedback: Haptic (mobile)
└── Release: Spring back 150ms

Swipe Actions
├── Gesture: Horizontal swipe (50px minimum)
├── Velocity threshold: 0.5 (points/ms)
├── Animation: 300ms ease-out snap
└── Usage: Delete photo, dismiss notification

Pull-to-Refresh
├── Gesture: Vertical drag (50px minimum)
├── Trigger: Downward 80px threshold
├── Loading: Spinner 4 seconds max
└── Completion: Spring back 200ms
```

### Motion Principles

```
1. Fast interactions feel responsive
2. Slow animations feel premium
3. Deceleration (easing out) = natural movement
4. Haptic feedback = tactile confirmation
5. Meaningful transitions = not distracting
6. Accessibility: Reduce motion setting respected
```

---

## 9. Dark Mode (Future)

```
Not required for MVP, but designed for scalability:

Color adjustments:
├── neutral-white → neutral-900 (backgrounds)
├── neutral-900 → neutral-50 (text)
├── Shadows: Increase opacity 0.5x
├── Accent colors: Lighten by 20%
└── Brand colors: Maintain saturation

Implementation:
├── CSS variables: --color-primary
├── React Native: useColorScheme()
├── System setting: Respect device preference
└── Manual toggle: Settings > Dark Mode
```

---

## 10. Accessibility

### WCAG 2.1 AA Compliance

```
Color Contrast
├── Normal text: 4.5:1 minimum
├── Large text (18px+): 3:1 minimum
├── UI components: 3:1 minimum
└── Test: WebAIM Contrast Checker

Typography
├── Minimum font size: 12px (readable without zoom)
├── Line height: 1.5+ (readability)
├── Line length: 50-75 characters (readability)
└── Don't rely on color alone

Interactive Elements
├── Minimum size: 44px × 44px (touch target)
├── Spacing: 8px minimum between touch targets
├── Focus indicator: 2px outline (brand-primary)
├── Keyboard navigation: Tab order logical
└── Screen reader: Semantic HTML + aria labels

Animations
├── Respect prefers-reduced-motion setting
├── No flashing (>3x/second)
├── Pausable animations
└── No motion-triggered actions
```

### Localization

```
Right-to-Left (RTL) Languages (Future)
├── Text direction: Auto-flip
├── Icons: Mirror specific icons (arrow, chevron)
├── Spacing: Reverse left/right padding
├── Numbers/dates: Locale-specific formatting
└── Testing: iOS/Android RTL locale support

Turkish Localization (Current MVP)
├── Font: Include Turkish characters
├── Button text: Capitalize all words
├── Date format: DD.MM.YYYY
├── Currency: ₺ symbol (right side)
└── Page direction: LTR (left-to-right)
```

---

## 11. Brand Usage Guidelines

### Logo Usage

✅ DO:
```
├── Use on brand-primary background only
├── Maintain clear space (1.5x logo width)
├── Use minimum 80px width
├── Stack horizontally (preferred)
└── Use official color values exactly
```

❌ DON'T:
```
├── Don't stretch or distort
├── Don't use in outline/stroke only
├── Don't place on patterned backgrounds
├── Don't change colors
└── Don't rotate or skew
```

### Color Usage

✅ DO:
```
├── Use primary for CTAs and focus states
├── Use secondary for premium/featured content
├── Use accent for milestones/special moments
├── Maintain neutral backgrounds for readability
└── Use semantic colors for status (green = success)
```

❌ DON'T:
```
├── Don't use pure black (use neutral-900)
├── Don't use more than 3 brand colors in view
├── Don't low contrast text
├── Don't use colors for information alone
└── Don't mix brand colors for decoration
```

---

## 12. Implementation Checklist

### For Design Team (Figma)

- [ ] Create master component library
- [ ] Document all components with specs
- [ ] Create iOS (SF Pro) and Android (Roboto) variants
- [ ] Design 10 album template variants
- [ ] Create animation storyboards
- [ ] Set up design tokens (colors, spacing, typography)
- [ ] Create design system documentation (Figma wiki)
- [ ] Design landing page (desktop only)
- [ ] Create onboarding flow (6 screens)
- [ ] Design profile + settings screens

### For Development Team

- [ ] Extract design tokens to code (CSS variables)
- [ ] Implement component library (React Native Paper)
- [ ] Configure Tailwind/styled-components with design system
- [ ] Setup typography system (font loading, sizing)
- [ ] Implement shadow system
- [ ] Setup accessibility (contrast, ARIA labels)
- [ ] Configure animations/transitions
- [ ] Test on iOS/Android devices (notch safety)
- [ ] Test dark mode (if implemented)
- [ ] Verify WCAG 2.1 AA compliance

---

**Status**: ✅ Design system complete, ready for Figma implementation
