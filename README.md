# DMIT PalmSpring: $100/Year for 2 vCPU and 2TB on a CN2 GIA Return Route — Specs, Real Stock Odds, and How It Compares

PalmSpring sounds like a data center. It isn't one. It's a plan code inside DMIT's Los Angeles Premium lineup, and it appears on the order page as **PVM.LAX.Pro.PalmSpring**. That naming habit explains most of the confusion: people search for it expecting a location page and land instead on a VPS that is famous less for its specs than for how often it's out of stock.

So the search query is really three questions. What do you get for $100 a year. Why does it keep vanishing. And is it better than the cheaper, always-available plans sitting next to it in the same store.

## What PalmSpring actually is

DMIT has run this plan as a recurring limited release rather than a permanent SKU. The first batch showed up as a summer promotion in August 2023 at $100/year, and DMIT has restocked it in waves ever since — April 2025 alongside **LAX.Pro.MALIBU**, June 2025 alongside **LAX.Pro.Irvine**, and again later in the summer. Roundups published in 2026 have listed it as in stock at points, which is the tell: this plan's availability is a moving target, not a fixed state.

It sits in the Premium (Pro) tier, which at DMIT means the China-optimized network. The three tiers are worth memorizing before you compare anything, because the price gap between them for identical hardware is bigger than the gap between most configuration levels:

- **Premium (Pro)** — Tier 1 transit plus DMIT's own backbone plus China Telecom's CN2 GIA. Top price, made for mainland-facing traffic.
- **Eyeball (EB)** — CMIN2/CMI "best effort" China optimization. Middle price.
- **Tier 1 (T1)** — pure international BGP, no China-specific routing. Cheapest by a wide margin.

PalmSpring is the Pro entry point that undercuts the official baseline for that tier.

## The specs, and where the $100 goes

| Item | What the plan ships |
| --- | --- |
| CPU | 2 vCPU (AMD EPYC; batches have shown EPYC 7002/7003 series, and newer hardware generations have appeared in later restocks) |
| RAM | 2 GB |
| Storage | 40 GB SSD |
| Traffic | 2000 GB / month, counted in both directions |
| Port | 2 Gbps VirtIO |
| IPs | 1 IPv4 + 1 IPv6 /64 |
| Billing | $100 / year, or $39 / quarter |
| Order page status | 3 hours of unpaid order time before automatic cancellation |

Two details in that table matter more than they look.

**Traffic is billed both ways.** DMIT counts upload and download toward the same quota, so a 2 TB monthly allowance behaves closer to 1 TB each way. If your workload is asymmetric — a mostly-downloading site, a file mirror, a media relay — overage will find you faster than a marketing page might suggest.

**Quarterly billing exists but is bad value here.** $39 per quarter works out to $156 a year. The annual cycle at $100 is the only sensible option for this plan, and it's also the reason it gets bought out in hours.

👉 [Check current PalmSpring pricing and stock](https://www.dmit.io/aff.php?aff=12046&pid=182)

## The routing is the actual product

You are not paying $100 for 2 vCPU and 40 GB of SSD. Plenty of providers sell that for under $5 a month. You're paying for the route, and for the Pro tier that path is specific:

**IPv4**
- China Telecom: outbound via CTG GIA, which is CN2 GIA (AS4809)
- China Unicom: outbound via CUG, the 9929 premium path
- China Mobile: outbound via CMIN2 (AS58807)
- All three carriers: return traffic forced onto CN2 GIA

**IPv6**
- Return routing across the board goes through CMIN2, not CN2

That last line is the one most write-ups skip. DMIT's LAX Pro IPv6 is optimized, but it is not CN2, so v6 performance crossing the border runs weaker than v4. If your application prefers IPv6 or you're testing dual-stack, expect a difference and plan around it.

The published test range for this location is 154.17.6.0/24, and DMIT runs per-location Looking Glass endpoints, which is the honest way to check latency from your own ISP before buying rather than trusting anyone's benchmark chart.

## What happens when you blow through 2 TB

This is one of the few genuinely unusual things about DMIT's LAX Premium plans: running out of traffic doesn't take the machine offline. The port gets throttled instead, and the server keeps answering.

For the $100/year class, community reports put the throttled speed at roughly 4 Mbps. It's slow enough that you'll want to buy extra traffic or upgrade if it happens on a production site, but it also means a traffic spike at 3 a.m. doesn't turn into a support ticket and an outage. Note that other DMIT product lines handle exhaustion differently — the Tokyo Premium plans suspend instead of throttle — so don't carry the assumption across locations.

## Small print worth reading before you pay

A few of these rules have bitten people, and they're all published:

- **Free IP replacement every 15 days** if your IP gets blocked. That's a real difference from providers who charge per swap, and it matters if you're running anything that attracts blocking.
- **SSH is key-based by default.** After ordering, you download a key bundle from the panel and log in with the provided key file. If you're used to password auth, budget the extra ten minutes, including the internal debate about whether to reconfigure it.
- **Refunds: 3 days, under 30 GB.** Full refund (minus gateway fees) within 3 days of purchase if you've used less than 30 GB of traffic. Partial refund is possible within 30 days, calculated from either remaining time or remaining traffic — whichever figure works out higher for DMIT.

One source describing the policy says the threshold is 10 GB rather than 30; the 30 GB figure appears in the refund rule text itself, including in non-DMIT reseller write-ups, so treat 30 GB as the working number but confirm on the order page. Some conditions void refunds outright: targeting (D)DoS, abuse, complaints about "the network not being good enough," IP geolocation, and a third refund request on the same product family.
- **New accounts can face an anti-fraud delay.** Buyers have reported needing to wait before a freshly registered account can complete an order. It doesn't require the original email, but it does mean "I'll sign up and grab one in the next restock" can run into a wall at the wrong moment. If you're planning to buy, register early.
- **Payment methods**: Alipay, WeChat Pay, PayPal, and cryptocurrency.

## The full plan list — all three profiles, all three locations

DMIT's catalogue is large enough to be genuinely annoying: three data centers, three network profiles, and two hardware platform generations, which multiplies into dozens of SKUs. Here's the structure, starting with the Los Angeles Premium family PalmSpring belongs to.

### Los Angeles Premium — limited-run plans

| Plan | CPU / RAM / SSD | Traffic and port | Price | Order |
| --- | --- | --- | --- | --- |
| LAX.Pro.PalmSpring | 2 vCPU / 2 GB / 40 GB | 2000 GB @ 2 Gbps | $100 / year ($39 quarterly) | [Order PalmSpring](https://www.dmit.io/aff.php?aff=12046&pid=182) |
| LAX.Pro.Irvine | 2 vCPU / 2 GB / 40 GB | 3000 GB @ 5 Gbps | $159 / year | [See Irvine availability](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.MALIBU | 1 vCPU / 1 GB / 20 GB | 1000 GB @ 1 Gbps | $49.90 / year | [See MALIBU availability](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.WEE | 1 vCPU / 1 GB / 20 GB | Listed as 0.5–0.8 TB @ 0.5–1 Gbps depending on batch | $39.90 / year | [See WEE availability](https://www.dmit.io/aff.php?aff=12046) |

### Los Angeles Premium — standard ladder

Prices below are monthly, for the current hardware generation pairing. DMIT sells some of these on an older platform (EPYC 7003 class) and some on a newer one (EPYC 9004/9005 class), and the newer one costs more for identical paper specs.

| Plan | CPU / RAM / SSD | Traffic @ port | Older platform | Newer platform | Order |
| --- | --- | --- | --- | --- | --- |
| LAX.Pro.TINY | 1 / 2 GB / 20 GB | 1000 GB @ 1 Gbps | $10.90 | $14.90 | [See TINY](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.Pocket | 2 / 2 GB / 40 GB | 1500 GB @ 4 Gbps | $16.90 | $21.90 | [See Pocket](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.STARTER | 2 / 2 GB / 80 GB | 3000 GB @ 10 Gbps | $34.90 | $43.90 | [See STARTER](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.MINI | 4 / 4 GB / 80 GB | 5000 GB @ 10 Gbps | $62.90 | $79.90 | [See MINI](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.MICRO | 4 / 4 GB / 160 GB | 7000 GB @ 10 Gbps | $87.90 | $110.90 | [See MICRO](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.MEDIUM | 6 / 8 GB / 160 GB | 15000 GB @ 10 Gbps | $199.90 | $289.90 | [See MEDIUM](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.LARGE | 8 / 16 GB / 320 GB | 25000 GB @ 10 Gbps | $499.90 | — | [See LARGE](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.GIANT | 12 / 24 GB / 640 GB | 50000 GB @ 10 Gbps | $1009.90 | — | [See GIANT](https://www.dmit.io/aff.php?aff=12046) |

LAX Pro plans throttle after quota rather than suspend. Throttle speeds step up with the plan size, from about 4 Mbps on the small end to 10 Mbps on the large ones.

### Every other ladder, and where it starts and tops out

| Location / profile | Entry | Top of the ladder |
| --- | --- | --- |
| LAX Premium (Pro) | TINY $10.90/mo | GIANT ~$1009.90/mo |
| LAX Eyeball (EB) | TINY $10.90/mo | GIANT ~$1009.90/mo |
| LAX Tier 1 | TINY $6.90/mo, WEE $36.90/year | GIANT ~$199.90/mo |
| HKG Premium (Pro) | TINY $39.90/mo | GIANT ~$759.90/mo |
| HKG Eyeball (EB) | from about $29.90/mo | — |
| HKG Tier 1 | TINY $6.90/mo, WEE $36.90/year | GIANT ~$199.90/mo |
| TYO Premium (Pro) | TINY $21.90/mo | GIANT ~$829.90/mo |
| TYO Tier 1 | TINY $6.90/mo, WEE $36.90/year | GIANT ~$199.90/mo |

Order any of these here: 👉 [Browse all DMIT plans and pricing](https://www.dmit.io/aff.php?aff=12046)

Two notes on that table. The Tokyo Eyeball series was discontinued, so TYO currently offers Premium and Tier 1 only. And every price above is list price as published in recent plan roundups — DMIT re-prices individual SKUs as hardware generations retire, so the order page is the only number that binds. Community trackers repeat this warning every few weeks because people keep getting surprised by it.

## PalmSpring vs Irvine vs MALIBU vs the regular TINY

The reason this plan sells out is arithmetic, and the comparison is short.

**PalmSpring at $100/year** buys 2 cores, 2 GB RAM, 40 GB SSD, and 2 TB monthly on a 2 Gbps port. **LAX.Pro.TINY**, the always-available official entry to the same Premium tier, costs $10.90/month — about $131 a year — for 1 core, 2 GB RAM, 20 GB SSD, and 1 TB on a 1 Gbps port. Same network tier, same location, and the limited plan is both cheaper and roughly double the machine. That's the whole story behind the stock problems.

**MALIBU at $49.90/year** is the cheapest way into LAX Premium, but you're buying 1 core, 1 GB RAM, 20 GB SSD, and 1 TB at 1 Gbps. Fine for a small static site or a relay. It is not fine for anything that wants RAM.

**Irvine at $159/year** keeps the PalmSpring hardware and raises the ceiling: 3 TB and a 5 Gbps port. You're paying $59 more for 50% more traffic and a much wider pipe. Worth it if you're actually pushing volume; overkill if you aren't, since the CPU and RAM don't change at all.

If your visitors are not in mainland China, none of these are your plans. **LAX Tier 1 TINY** is $6.90/month, and the annual **WEE** works out to roughly $3.08/month. You'd be paying a 2–4x premium for CN2 GIA routing you never touch.

## How to actually get one

PalmSpring is released in batches, and a batch is finite. The pattern that's repeated across restocks:

1. DMIT announces a restock, often bundled with another limited plan.
2. Stock clears within hours, and during busier restocks buyers queue.
3. Lists and trackers flip to "sold out," and resale listings appear on forums at or above cost.
4. Weeks or months pass, and the cycle repeats.

Practical moves that help: register your account and verify it well before a restock rather than during one, keep the PalmSpring plan page open and refresh during known promo windows, and use quarterly billing only as a stopgap. If it's gone when you look, **LAX.Pro.TINY** gets you the same Premium routing at a higher per-year cost, and **MALIBU** at $49.90/year is the cheapest route into the tier if your workload is light.

## Discount codes: read the fine print, or skip it

DMIT doesn't run a permanent public coupon. What circulates is a mix of time-limited codes and automatic annual discounts, and most of it is not for new buyers.

- `2025-EXISTING-CUSTOMER-10OFF` — 10% off, existing customers only, with a stated expiry of June 30, 2025. That date has passed, so treat it as historical unless DMIT revives it. It didn't apply to T1 series plans either.
- `202510_HKG_TYO_PRO_20OFF_RECURRING` — a recurring 20% off cited for Hong Kong and Tokyo Pro plans on quarterly or longer cycles. It appears in 2026 code roundups but is worth testing at checkout before you assume it applies to your order.
- **Automatic annual discounts** — recent plan write-ups note that annual billing on some LAX Pro SKUs discounts itself without a code, with the entry plan discounted most heavily. If a code box is empty and your cart total is lower than list, this is why.

The honest rule: the price shown on the order page after you pick a billing cycle is the real price, and it beats any coupon list you'll find on a blog.

## Who should buy it, and who shouldn't

Take it if you're hosting something with mostly mainland Chinese visitors, you want CN2 GIA return routing without paying the standard LAX.Pro ladder for it, and you're comfortable buying a year up front. The 2 cores and 2 GB handle a small production site, a bot, an API node, a relay, or a personal service without drama.

Skip it if your audience is international (buy Tier 1 and save 60%), if you need Hong Kong-level latency to southern China (that's HKG.Pro, starting at $39.90/month), if you want guaranteed RAM headroom for databases or JVM workloads, or if you can't tolerate a stock-out window between restocks.

The last consideration is the one that decides it for most people. PalmSpring is a good deal that you cannot reliably buy on demand, and if your project has a launch date, a plan you can't order is worth less than a slightly worse plan you can.
