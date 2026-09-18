# real estate lead qualification chatbot: how to sort buyers, sellers and renters automatically and book showings while you sleep

A lead texts you at 11:40 PM about a listing. You see it at 7:15 the next morning. By then they've messaged three other agents, and the conversation is already over. That's the scenario a real estate lead qualification chatbot is supposed to fix, and it's also the scenario where most bots quietly fail, because they treat a motivated seller, a tenant-buyer with no down payment, and a wholesaler fishing for inventory as the same conversation.

This piece is about what actually has to happen inside a real estate lead qualification chatbot for it to be worth the money, what to ask each lead type, and where a purpose-built tool like CloseBot fits — including what it costs and where it stops.

## What the bot is supposed to do before it "qualifies" anyone

Qualification gets talked about as a single step. In practice it's three, and skipping the first one is why so many real estate AI builds produce garbage data.

1. **Identify the lead.** A human receptionist answers this in four seconds: who is this? Agent, seller, buyer, renter, wholesaler, lender, spam.
2. **Qualify according to type.** A seller gets asked about condition, timeline and mortgage balance. A tenant-buyer gets asked about down payment and monthly comfort. Asking the same questions to both wastes everyone's time.
3. **Route or book.** Either hand it to a human with a reason-for-reaching-out summary, or book a showing/call directly on the calendar.

CloseBot's own documentation frames this around "Job Flows" — a drag-and-drop flow where you define objectives the agent works through step by step, rather than one giant prompt you hope behaves. For real estate specifically, the company has published a full live-build walkthrough for an investor handling eight lead types, which is worth reading if you want to see how the routing logic is actually wired.

## Step one: figure out who's talking, using tags instead of branches

Here's the mistake that breaks most real estate bots, and it's a technical one with real consequences.

The intuitive approach: trigger the bot on every inbound message, use one node to figure out the lead type, then branch off to separate paths for seller, buyer, agent, and so on. The problem is that in most builders, once a contact moves to a node, they stay there. Exit someone into the "seller" path and that's where they live forever, even after the conversation reveals they're actually a realtor.

Real estate contacts change type. The "seller" who turns out to be an agent. The tenant-buyer who inherits a property six months later. The buyer who becomes a seller.

The fix is to route on **CRM tags** instead of branching nodes. When the AI figures out mid-conversation that this is an agent, it updates the contact type field, a CRM workflow swaps the tag, and on the next message the contact simply stops matching the filter. The bot goes quiet by itself. One agent node, and the CRM data does the routing.

Two practical notes that come out of this setup:

- **Filters need maintenance.** If the bot replies when a contact is tagged `type-seller`, `type-tenant buyer prospect`, or has no type tag at all, then every new lead type you add later has to be added to that "is not" list too. Nothing will remind you.
- **Filtered-out leads hear silence.** Once someone gets tagged as a wholesaler and drops out of the filter, they get no reply at all and have no idea why. A canned response on that tag — "stepping away, someone will be with you shortly" — costs nothing and prevents a weird experience.

## What to ask each lead type

This is the part where generic BANT scripts fall apart. Real estate isn't one funnel.

### Sellers (and why order matters)

Motivated sellers are usually the highest-value lead, and the biggest risk is that the bot interrogates them. Someone describing an inherited property or a distressed situation is telling you a story before they're describing a transaction. Reassure and listen first, then collect:

- Property address — the one genuinely mandatory field
- Timeline to sell
- Reason for selling
- Condition and repairs needed
- Whether it's already listed with an agent
- Mortgage balance
- An open-ended "what are you hoping to do next?"

That last one earns its place. "I want to sell and move closer to my daughter in Tucson" tells you more about motivation than any dropdown menu.

### Tenant-buyers and seller-finance buyers

These are the same person whether they arrived from a rent-to-own listing or an owner-financed one. What changes is the property and the down payment expectation — owner financing generally wants more down.

The hard part isn't the questions, it's trust. Someone has to get comfortable enough to be honest about what they have available for a down payment, what other assets they could liquidate, and whether other real estate is in the picture. That's a warm-but-investigative instruction, and it's worth rewriting until it sounds like a person rather than a form.

### Buyers

Location at the micro-market level beats "the city," budget as a range rather than an exact number, property type, whether it's end-use or investment, timeline, and financing readiness. Ask for the phone number *after* they've invested a few answers, not before.

### Agents, wholesalers, cash buyers

These mostly need a reason-for-reaching-out summary passed along to a human. Some brokers deliberately don't want AI touching certain categories at all, which is a legitimate configuration, not a failure.

## The tools that make qualification credible

A bot that only asks questions is a form with extra steps. What changes the conversation is being able to answer back with real information inside the first few messages.

**Live property data.** CloseBot ships a property details tool that takes an address and pulls county records plus a market-adjusted value estimate. For an investor or agent, that means the agent can confirm beds, baths and square footage back to a seller immediately — which builds credibility fast, and occasionally surfaces something useful, like an addition that was never permitted and never made it into the record. Real estate was CloseBot's original use case; the company says its agents access over 100 million US property data points, and that the property data tools are included at no additional cost on any plan. They cover the United States only — everything else, including qualification and booking, works internationally.

**Current inventory.** If buyers are asking what's available, keep a live Google Sheet of listings in a connected Drive folder. Update the sheet, and the agent's answers update with it. When the sheet doesn't cover something, the instruction can fall back to the property lookup tool.

**A tag that makes your phone ring.** When a seller sounds motivated, the price sounds reasonable, and the property isn't already listed, the agent adds a tag like `VIP seller` and says something it can actually deliver: "Let me see if I can connect you with the listing agent right now." That tag fires a CRM workflow that initiates the call. Motivation detected plus instant call connection is about as close to an automated acquisitions desk as most teams will get this year.

**Smart FAQ.** When the agent can't answer something, it flags the question instead of inventing an answer. You answer once, and the agent can follow up with every lead who asked. This is the feature that prevents the classic disaster of an AI hallucinating a discount or a price that doesn't exist.

## Timing is the whole argument for a chatbot

CloseBot published a benchmark analysis of more than 1.1 million appointments booked by its agents, and the timing findings are the most useful part of it for anyone deciding whether to automate.

> Just over half of all bookings land outside 9-to-5 business hours, in the lead's own local time. About 11% happen between midnight and 6:00 AM — roughly the same share the entire day of Saturday produces.

If your coverage stops at 5 PM, you're not competing for the other half of the market. You're not in the game.

The other numbers worth knowing before you build a budget:

- **About 132 messages per booking** is the booking-weighted weekly average, counting inbound messages and leads who never respond. If you're quoting a client, multiply that by your per-segment SMS cost — the mistake is modelling on converting leads only.
- **Sunday is the cheapest day to convert**, taking about 29% fewer messages per booking than Friday, despite producing the lowest volume. Someone replying at 9 PM on a Sunday chose to be in that conversation.
- **Roughly 12% of bookings involve more than one channel.** Because those conversations tend to finish on SMS, a last-touch report makes the channel that started them look worthless. Treat each channel as a separate thread and one lead in eight has to repeat themselves — the fastest way to lose a warm one.
- **One lead in the dataset booked 355 days after first contact**, from a follow-up sequence that never stopped. Set follow-up windows in months, not days.

For a real estate team, that last point is the one most likely to pay for the tool by itself. Database reactivations of leads you wrote off two years ago are exactly where a patient bot outperforms a busy human.

## What CloseBot costs

CloseBot's pricing sits on top of the platform fee, with message usage varying by plan. Here's the current structure as published on its plans page and billing documentation:

| Plan | Price | Billing cycle | Key inclusions | Get started |
| --- | --- | --- | --- | --- |
| **Free** | $0 | Always free | 1 agent, 1 user seat, 100 messages/month, 1MB knowledge storage, unlimited account connections, property data tools | Start the free CloseBot account |
| **Core (Business)** | $64/mo, or $53/mo billed as $640/yr | Monthly or annual | 1 agent (works across unlimited accounts in one niche), 500 messages included, adjustable message ceiling, human support, additional agents/storage/seats at extra cost | See the Core business plan |
| **Agency** | $397/mo monthly, with an annual equivalent around $331/mo | Monthly or annual | Unlimited re-billable agents, white-label client portal, re-billing at your own markup, client wallets | Check the Agency plan |
| **Growth (custom)** | Custom quote | Custom | SLAs, HIPAA compliance, quarterly audits, priority 99.99% uptime, priority support, high volume | Request Growth plan pricing |

A few cost details that matter more than the headline:

- **Business plans include message costs in the base price.** Go over your ceiling and overage is drawn from a wallet at a higher per-message rate. Raising the ceiling monthly gets you into bulk pricing.
- **Agency accounts pay $0.012 per message** on the current plans page and re-bill it at whatever markup you set, with clients topping up a wallet that pays into your Stripe account. Extra user seats are $5 on both paid tiers.
- **Annual billing saves roughly 17%** and unlocks 50+ premium templates, per the plans page.
- **Every paid plan has a 7-day trial**, and the free plan stays free as long as you're under 100 messages a month. No credit card, month-to-month, no contract. There are no refunds, which is why the trial exists.

Worth being clear about which plan fits which situation: if you're an agent or investor running your own pipeline, Core is the relevant tier — the Agency plan's re-billing and white-label tools are for people selling AI services to clients, and you won't see that machinery on a Business account even during the trial.

## Where it falls short

Three honest caveats before you sign up for anything.

**Text only.** CloseBot handles SMS, website chat, email and other text channels. It does not do voice. If your leads expect phone calls, you're pairing this with something else. G2's pros-and-cons breakdown lists the lack of voice interactions among user complaints, along with occasional irrelevant answers.

**There's a learning curve.** Reviews on G2 consistently praise the drag-and-drop builder and the speed of setup, but the recurring counterpoint is that this is a sophisticated tool rather than a ten-minute install. You're writing instructions that read like an SOP for a new acquisitions assistant. That takes an afternoon.

**Watch the usage math.** The per-message rates are low, but at 132 messages per booking, a high-volume operation should model the wallet spend before committing. On the Agency plan it's re-billable, which changes the equation; on a Business plan it comes out of your margin.

## How to get to a working build this week

If you want to test the premise before committing real leads:

1. Create a free account and connect your CRM — native integrations cover HighLevel, HubSpot and LeadConnector, with an API and webhook route for custom stacks. Note that custom fields don't always re-pull immediately after connecting a source; if they're missing from your field list, refresh the screen.
2. Build one agent for one lead type. Sellers, if you're an investor or listing agent. Buyers, if you're on the buy side.
3. Write the instructions in sections, the way you'd brief a VA: what to check first, what to ask, what to do when the answer is bad news.
4. Use the testing portal with a persona attached, and turn on thinking mode so you can see the reasoning behind each reply before it goes anywhere near a real lead.
5. Publish, then watch. Keep a human takeover option available — the platform lets you pause the AI on any individual conversation.

One agent, one lead type, one afternoon. If a real estate lead qualification chatbot can't beat your current response time and your current question order on that narrow slice, a bigger build won't rescue it.
