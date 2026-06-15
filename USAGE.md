# How to Use the Marketing Email Generator

A step-by-step guide to generating, customising, and sending emails with this skill.

---

## 1. Install the skill

1. Open **Claude Code** on your desktop
2. Go to **Settings → Skills**
3. Click **Install from file**
4. Select `marketing-email-generator.skill` from this folder
5. Done — the skill is now active

> **Updating the skill:** Whenever a new version of the `.skill` file is released, repeat these steps. Claude Code will replace the old version automatically.

---

## 2. Generate your first email

Just describe what you want in plain English. You do not need any special commands or syntax.

**Minimum prompt:**
```
create a marketing email for the Vitamins Test (B12, Folic Acid, D, E & Q10)
```

**Claude will automatically:**
- Detect the email type (marketing, flow, announcement, etc.)
- Load your brand defaults (GetTested logo, social links, colours)
- Write the copy, fill the template, and save a `.html` file
- Tell you the file path and the subject line suggestion

---

## 3. Choose an email type (preset)

Add the email type to your prompt and Claude picks the right layout.

| Email type | What to say | Layout |
|-----------|------------|--------|
| **Marketing / promo** | "create a marketing email for X" | Hero + copy + features + CTA card |
| **Flow / automation** | "create a flow email for X" | Personal copy + single button (no feature boxes) |
| **Announcement** | "create an announcement for X" | Hero + image + copy + features + CTA |
| **Quiz result** | "create a quiz result email for X" | Personalised result style |
| **Re-engagement** | "create a re-engagement email for X" | Humble, low-pressure, social proof |
| **Newsletter** | "create a newsletter about X" | Letter-from-founder style |

If you do not specify a type, Claude defaults to `marketing`.

---

## 4. Add optional sections

Append any of these flags to your prompt:

| Flag | What it adds |
|------|-------------|
| `with video` | Clickable video thumbnail with play button |
| `with image` | Full-width product image block |
| `with signature` | Patrik's photo, name, title, and social links |
| `no signature` | Forces signature off |
| `minimal` | Strips feature boxes and CTA card — copy and button only |
| `with A/B subject` | Returns two subject line options for split testing |

**Examples:**
```
create a marketing email for the Iron Test, with video and signature
```
```
create a flow email for new subscribers, minimal, with A/B subject
```
```
create an announcement for our new DNA Test, with image, no signature
```

---

## 5. Reference brand assets by name

Instead of pasting image URLs, use the short asset name from the registry.

| Asset name | What it is |
|-----------|-----------|
| `logo-with-name` | Full GetTested logo (default) |
| `logo-icon-only` | Icon only variant |
| `sender-patrik-1` | Patrik photo option 1 (default signature photo) |
| `sender-patrik-2` | Patrik photo option 2 |
| `sender-patrik-3` | Patrik photo option 3 |
| `sender-patrik-4` | Patrik photo option 4 |
| `sender-patrik-5` | Patrik photo option 5 |
| `sender-patrik-6` | Patrik photo option 6 |
| `img-*` | Product images (add your own to assets.md) |
| `vid-*` | Video thumbnails (add your own to assets.md) |

**Example:**
```
create a marketing email for the Vitamins Test,
with signature, use sender-patrik-3 and img-vitamins-test
```

---

## 6. Open and preview the email

After Claude generates the email, it saves a `.html` file in your working directory.

1. Find the file path in Claude's response (e.g. `D:\gtd-skills\gettested-marketing-vitamins-test-email.html`)
2. Open it in any web browser — it shows exactly how it will look
3. Check on both desktop and mobile (resize your browser window)

---

## 7. Fill in the variables

Every generated email has a **configuration block at the very top** listing all variables.
This is the only place you need to edit for each campaign.

```html
<!--
=======================================================
  EMAIL CONFIGURATION — edit values here to customise
=======================================================

  PRODUCT:    {{product_name}}   = Vitamins Test (B12, Folic Acid, D, E & Q10)
  CTA URL:    {{cta_url}}        = https://gettested.io/vitamins-test
  CTA LABEL:  {{cta_label}}      = Order my vitamins test
  ...
=======================================================
-->
```

**To reuse the same email for a different campaign:**

Open the file in any text editor (Notepad, VS Code), update the values in the config block,
then do a global find-replace to push the new values through the HTML.

In VS Code: `Ctrl + H` → find `{{cta_url}}` → replace with the new URL → Replace All.

---

## 8. Send via your ESP

### Klaviyo
1. Go to **Content → Templates → Create Template**
2. Choose **Code Editor**
3. Paste the full HTML
4. Replace `{{customer_first_name}}` with `{{ first_name|default:"there" }}`
5. Replace `{{unsubscribe_url}}` with `{{ unsubscribe_url }}`
6. Save and preview

### Mailchimp
1. Go to **Campaigns → Email Templates → Code your own**
2. Paste the full HTML
3. Replace `{{customer_first_name}}` with `*|FNAME|*`
4. Replace `{{unsubscribe_url}}` with `*|UNSUB|*`
5. Save and test

### Manual / other ESP
1. Replace all remaining `{{variable}}` tokens with real values
2. Upload the HTML to your ESP's template editor
3. Map unsubscribe and tracking variables as required by your provider

---

## 9. Update brand details or add new assets

The skill stores brand config in two files inside the `.skill` archive.

**To edit them:**

1. Rename `marketing-email-generator.skill` to `marketing-email-generator.zip`
2. Extract the zip
3. Edit the relevant file:
   - `references/brand.md` — brand name, colours, social links, default sender
   - `references/assets.md` — add new product images, videos, or banners
4. Re-zip the folder
5. Rename back to `.skill`
6. Reinstall in Claude Code

**Adding a new product image:**
```
| img-iron-test | https://your-supabase-url/iron-test.jpg | Iron Test kit |
```

**Adding a YouTube video:**
```
| vid-how-it-works | abc123xyz | https://img.youtube.com/vi/abc123xyz/maxresdefault.jpg | How the test works |
```

Once added, reference it by name in any future prompt.

---

## 10. Example prompts reference

```
# Basic marketing email
create a marketing email for the B12 Test

# Marketing with video and signature, specific photo
create a marketing email for the Vitamins Test,
with video, with signature, use sender-patrik-2

# Flow email for post-purchase sequence
create a flow email for customers who just ordered the Iron Test

# Announcement with image
create an announcement email for our new DNA Health Test launch, with image

# Re-engagement, minimal layout
create a re-engagement email for subscribers inactive for 90 days, minimal

# Newsletter with video and A/B subject lines
create a newsletter about the importance of Vitamin D in winter,
with video, with A/B subject

# Quiz result email
create a quiz result email for customers who completed the health assessment quiz
```

---

## Quick reference card

```
PRESETS          marketing · flow · announcement · quiz-result · re-engagement · newsletter
MODIFIERS        with video · with image · with signature · no signature · minimal · with A/B subject
ASSET NAMES      logo-with-name · logo-icon-only · sender-patrik-1 to 6 · img-* · vid-*
CONFIG BLOCK     top of every HTML file — edit values there to customise per campaign
ESP TOKENS       Klaviyo: {{ first_name }} · Mailchimp: *|FNAME|* · Unsubscribe: replace {{unsubscribe_url}}
```
