# Marketing Email Generator — Claude Skill

A Claude Code skill that generates complete, ready-to-send HTML marketing emails from a single prompt. Built on a polished branded template with support for multiple email types, dynamic variables, video thumbnails, personal signatures, and more.

---

## What it does

You describe the email you need. Claude picks the right layout, writes the copy, fills in the HTML, and saves a complete `.html` file you can open in a browser, upload to your ESP, or send as-is.

Every generated email includes a **configuration block at the top** so you can swap the product, URL, or button label for the next campaign without touching the HTML.

```html
<!--
=======================================================
  EMAIL CONFIGURATION — edit values here to customise
=======================================================
  PRODUCT:    {{product_name}}   = Vitamins Test (B12, Folic Acid, D, E & Q10)
  CTA URL:    {{cta_url}}        = https://custom-supplements.com/vitamins-test
  CTA LABEL:  {{cta_label}}      = Order my vitamins test
  ...
=======================================================
-->
```

---

## Documentation

| File | Contents |
|------|---------|
| [USAGE.md](./USAGE.md) | Step-by-step guide — install, generate, preview, send via ESP, update assets |
| [vitamins-test-email.html](./vitamins-test-email.html) | Full example output |

---

## Installation

1. Download [`marketing-email-generator.skill`](./marketing-email-generator.skill)
2. Open **Claude Code** → Settings → **Skills** → Install from file
3. Select the `.skill` file
4. Done — Claude will now use this skill automatically when you ask for an email

---

## Usage

Just describe what you need in plain English. No special commands required.

```
create a marketing email for the Vitamins Test (B12, Folic Acid, D, E & Q10)
```

```
create a flow email for post-purchase B12 customers, with signature
```

```
create an announcement email for our new Iron Test launch, with image and video
```

```
create a re-engagement email for inactive customers, minimal, with A/B subject lines
```

---

## Email presets

The skill detects the email type from your prompt and picks the right layout automatically.

| Preset | Trigger phrase | Layout |
|--------|---------------|--------|
| `marketing` | "marketing email", "promo email", "campaign" | Hero + copy + features + CTA card |
| `flow` | "flow email", "automation", "sequence", "drip" | Personal copy + single CTA (no feature boxes) |
| `announcement` | "announcement", "launch", "new product" | Hero + image + copy + features + CTA |
| `quiz-result` | "quiz result", "personalised", "formula ready" | Post-quiz personalised result style |
| `re-engagement` | "re-engagement", "win-back", "we miss you" | Humble, low-pressure, social proof |
| `newsletter` | "newsletter", "update", "roundup" | Letter-from-founder style with dividers |

---

## Modifier flags

Add these to any preset to change what sections are included.

| Flag | Effect |
|------|--------|
| `with video` | Adds a clickable video thumbnail with play button overlay |
| `with image` | Adds a full-width product image block |
| `with signature` | Adds a personal sender signature (photo, name, title, social links) |
| `no signature` | Forces signature off even if the preset recommends one |
| `minimal` | Strips feature boxes and CTA card — keeps copy and button only |
| `with A/B subject` | Returns two subject line options for split testing |

**Examples:**

```
create a marketing email for the Iron Test, with video, no signature
create a flow email for new subscribers, with signature, minimal
create a newsletter about Q2 health trends, with A/B subject
```

---

## Dynamic variable system

Every configurable value in the email uses a `{{variable}}` placeholder.
This means you can reuse the same HTML for multiple campaigns with a simple find-replace,
or let your ESP (Klaviyo, Mailchimp, HubSpot) substitute values at send time.

| Variable | Description |
|----------|-------------|
| `{{customer_first_name}}` | Recipient first name — set by your ESP |
| `{{product_name}}` | Product or test name |
| `{{cta_url}}` | Main CTA button URL (used in both buttons) |
| `{{cta_label}}` | Main CTA button label (used in both buttons) |
| `{{website_name}}` | Brand / company name |
| `{{support_email}}` | Support email address |
| `{{current_year}}` | Copyright year |
| `{{unsubscribe_url}}` | Unsubscribe link — set by your ESP |
| `{{video_url}}` | Video link (YouTube, Vimeo, etc.) |
| `{{video_thumbnail_url}}` | Video thumbnail image URL |
| `{{sender_name}}` | Sender full name (signature) |
| `{{sender_title}}` | Sender job title (signature) |
| `{{sender_photo_url}}` | Sender headshot URL (signature) |
| `{{social_linkedin_url}}` | Brand LinkedIn page |
| `{{social_instagram_url}}` | Brand Instagram |
| `{{social_facebook_url}}` | Brand Facebook |
| `{{social_youtube_url}}` | Brand YouTube channel |
| `{{social_website_url}}` | Brand website |

**YouTube thumbnail shortcut:**
```
https://img.youtube.com/vi/YOUR_VIDEO_ID/maxresdefault.jpg
```

---

## Available sections

Each section can be included or excluded per preset or modifier flag.

| Section | Presets | Notes |
|---------|---------|-------|
| Header / Logo | All | SVG logo or brand name text |
| Hero | marketing, announcement, quiz-result, re-engagement | Eyebrow + headline + subheadline + CTA |
| Body Copy | All | 2–3 paragraphs, personalised |
| Image Block | Optional (any) | Product photo, banner, illustration |
| Video Thumbnail | Optional (any) | Clickable thumbnail with CSS play button |
| Feature Boxes | marketing, announcement, quiz-result | 3-column icon + title + description |
| Info Card CTA | marketing, announcement, quiz-result | Gradient card with repeat CTA |
| Signature | Optional (any) | Photo + name + title + social links |
| Footer | All | Support link + copyright + unsubscribe |

---

## Brand configuration

Set your brand details once in `references/brand.md` inside the skill — Claude reads this automatically before every email so you never re-enter your logo, colours, social links, or default sender.

```
Brand name:      Custom Supplements
Website:         https://custom-supplements.com
Support email:   support@custom-supplements.com
Brand colour:    #0C8097
Default sender:  Patrik Johansson, CEO and Founder
Social links:    LinkedIn | Instagram | Facebook | YouTube | Website
```

To update: extract the `.skill` file (it's a zip), edit `references/brand.md`, and repackage.

---

## Asset registry

All hosted images, videos, and thumbnails are registered by name in `references/assets.md`.
Instead of pasting URLs every time, just use the asset name in your prompt:

```
create a marketing email for the Iron Test, use the img-iron-test image and vid-how-it-works video
```

Claude resolves the name to the URL automatically.

**Asset categories:**
- `logo-*` — logo variants (SVG embedded by default, PNG/dark also supported)
- `sender-*` — sender headshot photos
- `img-*` — product images and kit photos
- `vid-*` — video thumbnails and YouTube IDs
- `banner-*` — hero banners for specific email types

**How to host your assets:**

| Service | Best for |
|---------|---------|
| Cloudinary | Images + auto-resize (free 25GB) |
| AWS S3 + CloudFront | Full control |
| GitHub raw URLs | Quick testing: `https://raw.githubusercontent.com/user/repo/main/image.png` |

Always use HTTPS public URLs — email clients block authenticated or HTTP images.

---

## Skill file structure

The `.skill` file is a zip archive containing:

```
marketing-email-generator/
├── SKILL.md                         ← entry point + quality checklist
├── assets/
│   └── email-template.html          ← base template with full CSS
└── references/
    ├── brand.md                     ← brand identity, social links, default sender
    ├── assets.md                    ← named URL registry (images, videos, thumbnails)
    ├── presets.md                   ← 6 email types + modifier flags
    ├── sections.md                  ← HTML snippets for every section
    ├── variables.md                 ← {{variable}} table + config block
    └── copy-guide.md                ← tone, headlines, CTA labels, subject lines
```

Claude reads reference files on demand — only what is needed for each email type is loaded.

---

## ESP compatibility

The `{{variable}}` tokens work with all major email service providers:

| ESP | How to use |
|-----|-----------|
| **Klaviyo** | Upload HTML as-is. Map `{{customer_first_name}}` → `{{ first_name }}` |
| **Mailchimp** | Replace `{{variable}}` with `*\|FNAME\|*` etc. before upload |
| **HubSpot** | Replace with `{{ contact.firstname }}` syntax |
| **Custom / manual** | Find-replace each variable before sending |

---

## Example output

See [`vitamins-test-email.html`](./vitamins-test-email.html) for a full generated example:
- Preset: `marketing`
- Modifiers: `with video`, `with signature`
- Product: Vitamins Test (B12, Folic Acid, D, E & Q10)

---

## Screenshots

> Add screenshots of generated emails to the `screenshots/` folder and reference them here.

---

## Built with

- [Claude Code](https://claude.ai/code) — AI coding assistant
- Claude Skill system — modular, installable AI skills
- HTML email best practices (table-based layout, inline CSS, mobile responsive)
