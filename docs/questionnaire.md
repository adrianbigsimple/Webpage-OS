# Questionnaire Flow

Ask questions conversationally in rounds. Don't read this file out loud — use it as your guide. Adapt the phrasing to feel natural. After each round, summarize what you've heard back to the user before moving on.

---

## Round 0: Goal and Brand (ALWAYS first)

This round comes before everything else. What it surfaces drives the two biggest
decisions in the project: the **goal** picks the page archetype (Phase 4), and the
**brand** determines the design system (Round 2 and Phase 2). Asking this at the end
means inventing a palette you then have to throw away.

**0.1 What is this page for? What would have to happen for you to call it a success?**
   - This is the business goal, not the industry. "I'm a dentist" isn't an answer;
     "I want people to book appointments" is.
   - If the answer is vague, push once: "Three months from now, what do you want to
     be able to say?"
   - Required. No default — the archetype comes from this.

   Goal -> archetype mapping (`docs/landing-page-patterns.md`):

   | What they want | Archetype |
   |---|---|
   | Get contacted, booked, or quoted | Conversion-Optimized |
   | Sell a product directly | Hero-Centric |
   | Validate an idea before building it | Minimal |
   | Get hired (portfolio, freelance) | Storytelling |
   | Be trusted (legal, health, finance) | Trust & Authority |
   | Compete against known alternatives | Social-Proof-Heavy |
   | Explain a product that doesn't explain itself | Interactive Demo or Feature-Rich |

**0.2 Do you have brand guidelines, a brand book, or anything that defines your colors and fonts?**
   - Accepts: PDF, file path, Figma link, Notion link, or "no".
   - Local PDF: read it with the Read tool (it handles PDFs).
   - A URL: use the `web-reader` skill.
   - Extract and record: hex codes, font names, tone of voice, logo usage rules.
   - **If the user has a defined brand, those values OVERRIDE `ui-ux-pro-max`.** Never
     invent a palette on top of a brand that already exists.
   - Default: none -> Round 2 builds the system from scratch.

**0.3 Do you have a folder with your visual assets — logo, photos, icons?**
   - Ask for the **folder path**, not individual files. That's how people actually keep
     assets: a "Brand" or "Logos" folder, not memorized per-file paths.
   - Scan whatever they give you: `ls -R "<path>"`
   - Report what you found before moving on: "Found 3 logos, 12 photos, and a favicon."
   - Flag what's usable: logo as SVG or PNG with transparency, photos 1200px or wider.
   - Copy them into `site/public/images/` in Phase 4.
   - If they answer this, questions 14, 15, and 16 in Round 4 are already answered —
     don't re-ask them, just confirm what you found.
   - Default: none.

**0.4 Where does your brand live today?** (ask this ONLY if 0.2 and 0.3 came back empty)
   - "Are your colors, logos, or photos in Canva, Google Drive, Notion, Figma, or Dropbox?"
   - If they name a tool and an MCP for it is connected in the session, pull from it
     instead of asking them to describe their brand from memory:
     - **Canva** -> `list-brand-kits` returns the brand kit's palette and fonts
     - **Google Drive** -> `search_files` for the logo and photos
     - **Notion** -> `notion-search` for copy, content, or a brief they already wrote
     - **Figma** -> ask for the public file link and use `web-reader`
   - If they name a tool and no MCP is connected, say so plainly: "I don't have Canva
     connected in this session. You can connect it, or just hand me the files."
   - Don't turn this into a technical conversation. The user never needs to know what an
     MCP is — they say where their stuff lives, you work out whether you can reach it.
   - Default: skip.

**0.5 Does this page need to connect to something you already use?**
   - Give examples, not a technical list: "An online store, a booking calendar, your CRM,
     a mailing list, payments, analytics?"
   - If yes, ask **where** it lives — "Shopify", "Calendly", "Stripe" — and stop there.
     You work out the implementation yourself from `docs/integrations.md`.
   - Read `docs/integrations.md` before promising anything. It sets out the four levels
     (A: link out, B: build-time pull, C: vendor embed, D: live API) and which one applies
     to each integration. **Level D is out of scope for this repo** — if someone genuinely
     needs it, say so plainly and offer B or C.
   - **Never say "I connected your page through the MCP."** An MCP is a tool YOU use while
     building; the published page never talks to one. If you pulled a Shopify catalog, say
     that: "I read your store and put your 6 products on the page."
   - Don't ask for secret keys or admin tokens. No level A, B, or C needs one.
   - This shapes the archetype and the sections: a page with a product catalog looks
     nothing like a lead-capture page. Factor it into Q0.1 and into Phase 4.
   - Default: connects to nothing. Most landing pages don't need to.

After Round 0, summarize what you have: "Got it — the page is for [goal], and [I have
your brand / I'll design one]. Now the basics about the business."

---

## Round 1: The Basics (always ask)

1. **What's your business or project called?**
   - Required. No default.

2. **In one sentence, what do you do?**
   - Default: Infer from the name and context.

3. **Who are you trying to reach?**
   - Default: "General audience"
   - Follow up if vague: "Are these mostly young professionals, families, business owners...?"

After Round 1, summarize: "Got it — [business] helps [audience] with [service]. Let me ask about the look and feel."

---

## Round 2: Visual Direction

**Before asking anything here, check what Round 0 surfaced.**

- **If the user has a defined brand** (0.2 or 0.4 produced colors and fonts): invent
  nothing. Questions 5 and 7 become a confirmation, not a choice: "Your guidelines use
  #1B3A5C and Söhne. I'll apply those as-is — want me to propose something for what's
  missing?" Run `ui-ux-pro-max` only for the gaps: if they have a palette but no fonts,
  search fonts that pair with that palette.
- **If they have no brand**: follow the questions as written below and build the system
  from scratch.

Replacing a brand that already exists with a generated palette is the worst mistake you
can make in this phase. Users won't always correct you — sometimes they just leave.

4. **Do you have any websites you like the look of?**
   - If yes: Use `web-reader` skill to analyze them. Note colors, layout, typography, vibe.
   - Default: Skip, choose based on industry.

5. **Any color preferences, or should I pick based on your industry?**
   - **If Round 0 already produced the brand palette, skip this and confirm instead.**
   - Default: Use `ui-ux-pro-max` to recommend. Run: `python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<industry>" --domain color`
   - If search fails: Choose based on industry norms from `docs/design-guide.md`.

6. **Light or dark theme?**
   - Default: Light.

7. **What vibe should visitors get?**
   - Offer options: professional, playful, bold, elegant, minimal, warm, modern, edgy, luxurious.
   - Default: "Professional and approachable."

After Round 2, **PAUSE and present the design direction**: "Here's what I'm thinking — [color palette with specific hex codes], [font pairing with names], [general layout approach]. Sound good?"

**Wait for user approval before continuing to Round 3.** If the user wants changes, adjust and re-present until approved. This ensures the content questions in Round 3 are informed by the approved design direction.

---

## Round 3: Content

8. **What's the one thing you want visitors to do?**
   - Examples: sign up, book a call, buy something, learn more, get a quote.
   - Default: "Learn more / get in touch."

9. **What are 3-4 key things to highlight?**
   - These become the features/services section.
   - Default: Generate from business description + industry norms.

10. **Do you want a contact form on the page?**
    - If yes: What fields? (Name, email, message is standard. Phone? Company?)
    - Options:
      - **Simple (default):** A "mailto:" link styled as a contact section — no backend needed.
      - **Form with Formspree:** Free service, no backend needed. Tell the user: "Go to formspree.io, create a free account, create a form, and give me the form ID (it looks like 'xpznqkdl')." If user doesn't want to do this now, use mailto: as default and leave a TODO comment.
    - If user just wants an email link or phone number, that works too.

11. **Got a tagline or slogan?**
    - Default: Write one. Run through humanizer.

12. **Any testimonials, reviews, or social proof?**
    - Default: Create a placeholder testimonials section. Use realistic but clearly placeholder names.

13. **Any social media links to include?**
    - Instagram, X/Twitter, Facebook, LinkedIn, TikTok, YouTube, etc.
    - Default: Placeholder social icons in footer — user fills in the URLs later.

After Round 3, recap: "I have everything I need for content. A couple more technical questions."

---

## Round 4: Technical (keep brief)

**If Round 0 already gave you an assets folder, questions 14, 15, and 16 are already
answered.** Don't re-ask — confirm what you found: "I'm using the SVG for the logo, and
these three photos for the hero and services. Sound right?"

14. **Do you have a logo?**
    - Accept: file path, URL, or "no"
    - Default: Text-only logo using the business name with the headline font.

15. **Any specific images to use?**
    - Accept: file paths, URLs, or "no"
    - Supported formats: JPG (photos), PNG (logos with transparency), SVG (icons/logos), WebP (modern compression)
    - If the user provides URLs, download them: `curl -o site/public/images/photo.jpg "URL"`
    - Default: No stock photos. Use geometric patterns, gradients, or abstract decorative elements that match the design system.

16. **Do you have a favicon (the small icon in browser tabs)?**
    - Accept: file path, URL, or "no"
    - Default: Generate a simple favicon from the brand colors using `site/src/app/icon.tsx`.

17. **What language should the page be in?**
    - Default: Same language the user has been speaking in.
    - Note: All page content (headlines, body text, CTAs, meta tags) will be in the chosen language.

18. **Want me to deploy it to a live URL when we're done?**
    - Explain: "I can deploy it to Vercel — you'll get a link you can share with anyone."
    - Default: Yes.

---

## Handling "I don't know" / "You decide"

When the user defers any decision:
- **Colors**: Run ui-ux-pro-max color search for their industry + vibe.
- **Fonts**: Run ui-ux-pro-max typography search for their vibe keyword.
- **Copy**: Generate based on their answers, run through humanizer.
- **Layout**: Use proven section order: Hero > Features > Social Proof > CTA > Footer.
- **Style**: Match to their industry: law firm = refined/serif, tech startup = clean/modern, restaurant = warm/organic, creative agency = bold/experimental.
- **Contact form**: Use a mailto: link styled as a contact section.
- **Social media**: Add placeholder icons in footer.

Always tell the user what you chose and why, briefly: "I went with a warm palette — terracotta and off-white — because it fits the artisan food space well."

---

## After All Rounds

Summarize the full brief back to the user:
- **Page goal** and the archetype that follows from it
- **Where the brand came from**: the user's guidelines, pulled from Canva/Drive/Notion, or designed by you
- Business name and description
- Target audience
- Design direction (colors, fonts, vibe)
- Main CTA
- Contact method (form, mailto, phone)
- Key sections/features
- Social media links
- Assets (logo, images, favicon, or defaults)
- Page language
- Deploy: yes/no

Ask: "Does this capture everything? I'll start building once you give me the green light."

Then proceed to Phase 2 (Design System) in the CLAUDE.md workflow.
