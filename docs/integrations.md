# Integrations

What to do when the page has to connect to something — a store, a calendar, a CRM, a
payment processor, a mailing list.

## The distinction that governs everything here

**An MCP is a tool *you* use while building. It is not something the published page
connects to.** A visitor's browser never talks to an MCP. Two separate layers:

| Layer | Who acts | What an MCP does |
|---|---|---|
| **Build time** | You, while constructing the page | Reads the user's real data: products, prices, photos, copy |
| **Runtime** | The published page, with a visitor in front of it | **Nothing.** The page needs its own connection |

Never tell a user "I connected your page to Shopify through the MCP." You didn't. You
read their catalog and baked it into a static page, and the buy buttons point at
Shopify's checkout. Say that instead — it's both true and more impressive.

## The four levels

Every integration lands on one of these. Pick the lowest one that does the job.

**Level A — Link out.** A button that goes to their existing thing. No integration, no
credentials, nothing to break. For a landing page whose job is to send traffic somewhere,
this is the correct answer far more often than it sounds.

**Level B — Build-time pull, static output.** Read their data with an MCP or API while
building, render it in the page's own design, and link each item to wherever the
transaction actually happens. The page stays static and fast; the other system handles
money and state.

This is the sweet spot for this repo. It's the level that makes the page look like *their
brand* instead of a generic embed.

Its cost, which you must state to the user: **data is frozen at build time.** Prices and
stock reflect the moment you built. Refreshing means rebuilding.

**Level C — Vendor embed.** The vendor's own JS widget dropped into the page — Shopify's
Buy Button, a Calendly inline widget. Real interactivity, vendor-hosted logic, styled by
the vendor. Fast to add, but it will not match the design system, and it costs page weight.

**Level D — Live API at runtime.** The Next.js app queries the vendor on every request.
Live prices, real cart, real availability. Needs environment variables and server-side
code.

**Level D is out of scope for this repo.** A landing page that maintains a cart is an
ecommerce build, not a landing page, and the 6-phase flow is not sized for it. If a user
genuinely needs D, say so plainly and offer B or C instead of half-building D.

## By integration

### Store — Shopify, WooCommerce, Etsy, Gumroad

| Level | What the user gets |
|---|---|
| A | CTA links to their storefront |
| **B (default)** | Product section in their design, each item linking to that product's checkout URL |
| C | Shopify Buy Button — real cart, vendor-styled |

For **B**, you need from the user: the store domain, and which products to feature (all,
a collection, or a hand-picked few). If a Shopify MCP is connected, pull titles, prices,
images, descriptions and product URLs with it. If not, ask them to paste product URLs, or
read the storefront pages with `web-reader`.

Do not ask for Admin API credentials. A landing page never needs write access to a store.

### Scheduling — Calendly, Cal.com, Acuity

Level A or C. The booking URL as a CTA covers most cases; the inline widget is worth it
when booking *is* the page's whole purpose. Ask for the scheduling link.

### Contact and lead capture

Already handled in the questionnaire, Q10. `mailto:` by default, Formspree when the user
wants a real form. Don't invent a third path.

### Newsletter — Mailchimp, ConvertKit, Beehiiv

Level C, using the vendor's embedded form snippet — these are built for exactly this and
handle double opt-in and compliance. Ask for the embed code or the form URL.

Never hand-roll a signup form that POSTs to a mailing-list API from the browser. It leaks
the API key to anyone who opens devtools.

### Payments — Stripe, Mercado Pago

Level A: a Stripe Payment Link or Mercado Pago link behind the button. The vendor hosts
checkout, the page holds no keys, and nothing sensitive touches this codebase.

Never put a secret key in the frontend. If a user offers one, decline it and explain that
a payment link does the same job without the risk.

### Analytics — GA4, Plausible, Fathom

A script tag in `layout.tsx`. Ask for the measurement ID or site ID. Load it with
`next/script` and `strategy="afterInteractive"` so it stays off the critical path.

## Credentials

Ask only for what the chosen level actually needs, and prefer the level that needs least.

- **Publishable / storefront tokens** — fine. They are designed to be public.
- **Secret keys, Admin API tokens, passwords** — never. No level A, B, or C needs one.
  If a user volunteers a secret, tell them not to paste it and pick a different level.
- Anything that must reach the running app goes in `site/.env.local`, which `.gitignore`
  already excludes. Never hardcode a value into a component, and never commit `.env.local`.

## Reporting back

At the end of Phase 4, tell the user in plain terms what you wired and what its limits
are. For a Level B store:

> Your 6 products are on the page, pulled from your Shopify store. Each "Buy" goes
> straight to that product's checkout. Prices are from today's build — if you change a
> price in Shopify, tell me and I'll rebuild.

That last sentence is the part people need and never get told.
