---
layout: article
title: "The Experience Curve and the Making of TSMC"
description: "How experience curve pricing and Morris Chang's foundry model helped TSMC build its manufacturing lead."
date: 2026-11-16
tags:
  - Semiconductors
  - TSMC
  - Business Strategy
---

Semiconductor manufacturing is a very unforgiving business. A leading-edge fab costs tens of billions of dollars before it ships a single chip. TSMC alone guided [$40 to 42 billion](https://www.marketbeat.com/earnings/reports/2025-11-14-taiwan-semiconductor-manufacturing-company-limited-stock/) of capital spending for 2025. That money is committed years in advance, before anyone knows whether the process will work or whether the customers will come.

At first the process usually does not work well. A new production line starts with poor yields: only a small share of the chips on each wafer actually function. Dust, chemical impurities and drifting equipment kill dies, and every cause has to be found and fixed. When Morris Chang took over a new transistor line at Texas Instruments in 1958, its yield was [zero](https://commoncog.com/case/texas-instruments-learning-curve/). Four months of work brought it to 20%. Early sceptics of the integrated circuit made the arithmetic explicit: put 20 components with 90% yield each on one piece of silicon, and only about 12% of the circuits [survive](https://www.ias.ac.in/article/fulltext/reso/017/11/1100-1115).

The economics of the industry therefore come down to one question: how fast can a fab move from expensive, mostly defective output to cheap, reliable output? The company that gets there first can undercut everyone and still earn the returns that pay for the next fab. The company that gets there last owns equipment it may never pay off.

TSMC has answered that question better than anyone. Its answer rests on an idea from 1966, sharpened into a pricing strategy at Texas Instruments in the early 1970s, and finally built into the structure of a company.

## The experience curve

In 1966 Bruce Henderson, founder of the Boston Consulting Group (BCG), compared semiconductor price data with the industry's accumulated volume. In constant dollars, prices fell by about [25% with every doubling](https://bcg.com/publications/1973/corporate-finance-strategy-portfolio-management-experience-curve-reviewed-part-ii-the-history) of cumulative output. He called this the experience curve.

<figure>
  <a href="{{ '/images/tsmc-experience-curve.png' | relative_url }}"><img src="{{ '/images/tsmc-experience-curve.png' | relative_url }}" alt="Bar chart showing unit cost falling by 25% with each doubling of cumulative semiconductor output."></a>
  <figcaption>Illustration of a 25% experience curve, the rate Henderson found in semiconductor prices.</figcaption>
</figure>

The older learning curve, known from wartime aircraft production, covered only labour. Henderson's [claim](https://www.bcg.com/publications/1968/business-unit-strategy-growth-experience-curve) was broader: all costs, including materials, overhead, distribution and capital, fall by 20 to 30% each time cumulative production doubles. The implication was stark. If cost depends on cumulative volume, the firm with the largest market share has the lowest cost, and the gap widens over time. Henderson concluded that new products should be priced "as low as necessary to dominate their market segment or probably not be sold at all."

## BCG at Texas Instruments

Around 1970 Henderson approached Mark Shepherd, CEO of Texas Instruments, then the largest semiconductor company in the world. Shepherd agreed to a joint study. Henderson assigned his protégé Bill Bain to the account, and Shepherd assigned Morris Chang, who ran TI's integrated-circuit business.

The collaboration was close and data-heavy. By Chang's own account on the [Acquired podcast](https://www.acquired.fm/episodes/tsmc-founder-morris-chang), Bain worked from a small office next to his, flying in from Boston every Monday for about two years. Chang's role was to open TI's books: unit costs and prices for every family of transistors and integrated circuits the company made. Henderson's original curve rested on industry-wide prices. What Bain and Chang built rested on a single manufacturer's internal costs, which made it usable for decisions.

In 1973 Bain left BCG to found [Bain & Company](https://en.wikipedia.org/wiki/Bain_%26_Company), and TI followed him as a client. Chang is careful about his own part: he says he did not originate the theory, but helped refine it "to the point where a semiconductor company can use it effectively."

## Pricing for tomorrow's costs

The conventional way to price a chip was cost plus margin, with high early prices to recover the capital outlay. TI inverted this. It priced chips for the cost they would reach once volume ramped, which often meant selling below current cost. Chang called it [learning-curve pricing](https://commoncog.com/case/texas-instruments-learning-curve/); BCG called it experience curve pricing.

The logic runs back to yields. A line at low volume learns slowly, because there are few wafers through which to find and remove defects. A low price wins orders and runs the line at full capacity, so yields improve faster and unit costs fall to meet the price. The pricing decision is, in effect, a decision to buy learning.

The chart below illustrates the mechanics with a hypothetical 25% curve and a 60-cent selling price. Early chips are sold at a loss; past the break-even volume, each chip earns a margin.

<figure>
  <a href="{{ '/images/tsmc-pricing-break-even.png' | relative_url }}"><img src="{{ '/images/tsmc-pricing-break-even.png' | relative_url }}" alt="At a 60-cent selling price, unit cost falls below price after about 3.4 million chips."></a>
  <figcaption>Illustration, not historical data: a 25% curve starting at $1.00 a chip, with a 60-cent selling price.</figcaption>
</figure>

TI pushed the strategy aggressively, cutting prices every quarter whether or not customers asked. Of its 1974 price cuts on TTL logic chips, Chang said his aim was "to sow despair in the minds of my opponents." The industry expected margins above 50%. When TI, the lowest-cost producer, earned only 40% at its prices, competitors with smaller volumes concluded they could not make money at all.

The curve also made competitors legible. If every firm learns at roughly the same rate, a rival's unit cost can be read off your own curve at the rival's cumulative volume, and that volume can be estimated from market share. Henderson made the point in 1968: costs relative to competitors "can also be estimated." A firm with four times a rival's cumulative output sits two doublings further down the curve. At 25% per doubling, its unit cost is about 56% of the rival's.

The next chart shows this with hypothetical numbers: at a 70-cent price, the leader earns 14 cents per chip while the follower loses 30.

<figure>
  <a href="{{ '/images/tsmc-market-lead.png' | relative_url }}"><img src="{{ '/images/tsmc-market-lead.png' | relative_url }}" alt="At a 70-cent selling price, a producer with four million chips of cumulative output profits while a rival with one million loses money."></a>
  <figcaption>Illustration, not historical data: the same 25% curve, with the leader at 4M chips and the rival at 1M.</figcaption>
</figure>

The obvious objection is that any firm can read the same curve and cut prices the same way. It can, but the arithmetic is not symmetric. A follower that matches the leader's price loses money on every unit, because it sits higher on the curve, while the leader at that same price is still profitable. Matching the price does not close the gap either. Henderson [observed](https://www.bcg.com/publications/1968/business-unit-strategy-growth-experience-curve) that when competitors keep the same relative market shares, their costs "tend to move in parallel." Both firms slide down the curve, and the leader stays the same number of doublings ahead. The only way for the follower to catch up is to take share, which means pricing below the leader and losing even more per unit, for longer.

The strategy is therefore not a secret that works only while others are unaware of it. It is a race, decided by who starts with the most cumulative volume and who can fund losses the longest. That is why it favoured TI, the largest producer, and why Henderson argued that market share "must be maintained at all costs" while the market is growing. When no firm has a clear volume lead, everyone cutting at once produces a price war that nobody wins, which is what TI later met in calculators. A follower's real escape is to change the curve rather than race down it: a better process, or a new product generation where everyone's cumulative volume starts again from zero.

Used this way, price becomes a signal as much as a revenue line. Michael Porter [describes](https://strategyu.co/experience-curve/) TI announcing the price of a memory chip two years before it would ship. Motorola announced a lower price; two weeks later TI announced half of Motorola's. The other firms declined to enter, and TI won the market before any of them had committed capital to a fab.

## The foundry as a volume machine

Chang left TI with two ideas. One was the experience curve, and an understanding of how to use it. The other was a proposal TI had [rejected in 1976](https://superscout.co/innovation/pure-play-semiconductor-foundry): a manufacturer that designs no chips of its own and builds them for other companies. In 1985 Taiwan's government recruited him to build a domestic chip industry. Taiwan had little design talent and no global brands, but strong manufacturing discipline. In 1987 Chang founded TSMC as the first pure-play foundry.

The foundry model resolves the problem the experience curve poses. An integrated chipmaker accumulates volume only as fast as its own products sell, and carries the full capital and yield risk of every process node on that volume alone. A foundry aggregates demand from many designers on the same process. Its cumulative output doubles faster than any single customer's could, so yields mature faster and unit costs fall faster. Lower costs attract more customers, and the added volume both accelerates learning and funds the next node. Capital risk that would be prohibitive for one company is spread across the industry.

Intel, vertically integrated, built leading-edge capacity mainly for its own PC and server processors. TSMC built for Apple, Nvidia, Qualcomm and AMD, and its volume grew with the smartphone. When Apple chose ARM-based processors for the iPhone and moved their production to TSMC from 2013, that volume, [by one account](https://www.scmp.com/tech/big-tech/article/3098323/how-decision-15-years-ago-contributed-intels-fall-grace-today), let TSMC "pull ahead in manufacturing process technology." Intel's 10-nanometer process slipped in 2015 and its 7-nanometer process [in 2020](https://aragonresearch.com/intels-lost-decade-how-tsmc-took-the-chip-lead/). By then the leading edge of manufacturing had moved to Taiwan.

## Sources

- Bruce Henderson, ["The Experience Curve"](https://www.bcg.com/publications/1968/business-unit-strategy-growth-experience-curve), BCG, 1968

- Bruce Henderson, ["The Experience Curve Reviewed, Part II: The History"](https://bcg.com/publications/1973/corporate-finance-strategy-portfolio-management-experience-curve-reviewed-part-ii-the-history), BCG, 1973

- Reeves, Stalk and Scognamiglio, ["BCG Classics Revisited: The Experience Curve"](https://www.bcg.com/publications/2013/growth-business-unit-strategy-experience-curve-bcg-classics-revisited), BCG, 2013

- Acquired, ["TSMC Founder Morris Chang"](https://www.acquired.fm/episodes/tsmc-founder-morris-chang), January 2025

- Commoncog, ["Texas Instruments: Inventing Learning Curve Pricing"](https://commoncog.com/case/texas-instruments-learning-curve/)

- StrategyU, ["The experience curve: how BCG turned falling costs into a strategy"](https://strategyu.co/experience-curve/) (Porter's RAM story)

- Jack Kilby, ["Invention of the Integrated Circuit"](https://www.ias.ac.in/article/fulltext/reso/017/11/1100-1115), IEEE Transactions on Electron Devices, 1976

- [Bain & Company](https://en.wikipedia.org/wiki/Bain_%26_Company), Wikipedia

- Superscout, ["Pure-play semiconductor foundry"](https://superscout.co/innovation/pure-play-semiconductor-foundry)

- South China Morning Post, ["How a decision 15 years ago contributed to Intel's fall from grace today"](https://www.scmp.com/tech/big-tech/article/3098323/how-decision-15-years-ago-contributed-intels-fall-grace-today), 2020

- Aragon Research, ["Intel's Lost Decade: How TSMC Took the Chip Lead"](https://aragonresearch.com/intels-lost-decade-how-tsmc-took-the-chip-lead/)

- MarketBeat, ["TSMC Q3 2025 Earnings Call Transcript"](https://www.marketbeat.com/earnings/reports/2025-11-14-taiwan-semiconductor-manufacturing-company-limited-stock/), 2025
