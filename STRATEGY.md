# Pro 36 Solutions — Marketing Site Plan

**Purpose.** A public-facing site to spread awareness of the Pro 36 ops
platform and generate interest from other dog-training facilities, distinct
from `pro36-ops-platform` (the product itself) and `pro36-website` (marketing
for Justin's own facility, Pro 36 Canine Academy — a different audience: dog
owners, not facility operators).

**Status:** not started. This doc is the plan to react to before any code.

---

## Scope for v1

**Goal: pure marketing / lead-gen.** No live signup or checkout on the site
itself — self-serve signup + promo codes is a separate, not-yet-built
initiative (see `pro36-ops-platform` project memory). Until that ships, this
site's call-to-action is **request access / join the waitlist**, not "sign up
now." That also means this site can go live independently, well before the
self-serve work finishes.

**Audience:** dog-training facility owners/operators considering the
platform — not end clients (dog owners). Different reader than
`pro36-website`.

**Domain:** `pro36solutions.com` apex (+ `www`) — deliberately left
unclaimed during the ops-platform domain migration for exactly this
(`app.` already serves the product). See `pro36-ops-platform`'s
`DOMAIN-MIGRATION-PLAN.md`.

**Hosting:** static site, Netlify + Netlify DNS — same pattern as
`pro36-website` (plain HTML/CSS, no build step, no framework) and
`billing-portal`'s marketing pages. Keeps it simple to hand-edit and fully
decoupled from the ops app's Cloud Run deploys — a copy change here can never
break or block the product.

**Lead capture:** Netlify Forms (built into the hosting, no backend needed)
for a "request access" / contact form. Submissions land in the Netlify
dashboard (and can forward to email) — no new infra to stand up.

---

## Proposed page structure

Mirroring `pro36-website`'s shape, adapted for a B2B/facility-operator
audience:

1. **Home** — the pitch: what Pro 36 does, who it's for, the core wedge
   (program/curriculum tracking — what Gingr/Paw Partner don't do well per
   `STRATEGY.md`'s "why"), a primary CTA into the request-access form.
2. **Key features** — the actual feature set: leads/consults → enrollments →
   training logs/program checklists → weekly owner updates → billing.
   Screenshots from the ops-platform's existing demo tenant ("Sunny Paws Dog
   Training", `Business.isDemo` — already used for in-app tutorials, so it's
   populated with synthetic data purpose-built to be safe to show publicly,
   no scrubbing needed).
3. **Pricing** — informational only for v1 (no live checkout). Shows all 3
   standard tiers, from `BILLING-SAAS-PLAN.md` §2b:
   | Tier | Capacity | Price/mo |
   |---|---|---|
   | Solo | up to 4 | $79 |
   | Facility | 5–20 | $150 |
   | Enterprise | 21+ | $300 |
   **Founder ($25/mo) stays fully invisible on this site** — not a public
   offering, invite/code-only. See the promo-code note below.
4. **About / why Pro 36** — credibility angle: **built by trainers, for
   trainers** (not a solo-founder story — plural, team framing) solving a
   real problem in the industry, not a generic SaaS vendor guessing at it.
5. **Request access** — the form (Netlify Forms), doubles as the site's one
   real conversion goal for v1.

Open question: FAQ page, or fold that into Home/Key features? `pro36-website`
has a dedicated FAQ; may or may not be warranted yet with less content to
answer questions about.

---

## Founder pricing via promo code — folds into the signup initiative

Justin's call 2026-09-14: Founder pricing ($25/mo) should be reachable via
the same promo-code mechanism as trial codes, not a separate system — but a
Founder-granting code needs a **hard redemption cap of 3**, not just a
date window, so it can't be leaked and used beyond the 3-account cap Founder
pricing was always scoped to. This means the promo-code design (queued in
`pro36-ops-platform` project memory) needs two capabilities, not one:
- **date-windowed codes** (trial access, as already scoped), and
- **redemption-capped codes** (Founder pricing, max 3 total uses, no
  particular date window implied — capped by count, not time).

A code could plausibly need both a window *and* a cap; treat them as two
independent optional constraints on the same `PromoCode` model rather than
two separate code types. **This is a build note for `pro36-ops-platform`,
not this site** — flagging here since Founder pricing's public invisibility
is a marketing-site decision that depends on it.

---

## What I need from Justin before drafting real copy

- Any screenshots beyond the demo tenant's existing tutorial screens okay to
  use, or should this launch text-only until more are ready.
- Anything else on the page list to drop/add/reorder.

---

## Sequencing note

This site has **no dependency** on the self-serve signup + promo code
initiative and can ship first, exactly as planned. Its CTA just needs to
change once self-serve exists — "Request access" → "Start your trial" — a
copy change, not a rebuild.
