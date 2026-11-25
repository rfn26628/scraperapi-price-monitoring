# Price Monitoring: Build It With ScraperAPI or Buy a SaaS? What a Credit Actually Buys, Which Plan Fits, and When a Free Tracker Is Enough

A price monitoring setup costs either $49 a month or $149 a month, and those two numbers buy completely different things. Pricefy charges by SKU and hands you a finished dashboard with alerts, price history and repricing that starts at its Pro tier ($99/month, or $74 billed annually). ScraperAPI charges by credit and hands you raw JSON: $149/month buys 1,000,000 credits, an Amazon product page costs 5 of them, so the Startup plan covers roughly 200,000 Amazon fetches a month. No dashboard, no alerts, no repricing. You build those.

Which one is right comes down to three questions: how many products you watch, whether you need prices changed automatically or just observed, and whether you already have somewhere to put the data. The rest of this article works through the arithmetic that the pricing pages don't do for you.

> **Quick answer:** if you sell on Shopify or Amazon and want competitor prices plus automatic repricing, buy a monitoring SaaS and skip the engineering. If the prices need to land inside a system you already own (a pricing engine, a BI warehouse, a marketplace tool you built), ScraperAPI is the fetching layer, and **Startup at $149/month** is the sensible starting point for most teams: 1,000,000 credits, 50 concurrent threads, US and EU geotargeting. Measure your real credit burn for a month before moving up.
>
> 👉 [See every ScraperAPI plan and its current credit allowance](https://www.scraperapi.com/pricing?fp_ref=coupons)

## ScraperAPI plans and prices

ScraperAPI prices on credits, not on products or seats, and the annual discount is 10% across the board. Enterprise is quoted separately. The two mid-tier plans, Scaling and Professional, sit between Business and Advanced and are the ones that combine pay-as-you-go billing with auto-upgrade; their credit allowances and prices are shown on the pricing page as configured.

| Plan | Credits per month | Price (monthly / billed annually) | Concurrency and targeting | Sign up |
| --- | --- | --- | --- | --- |
| Hobby | 1,000 | Free | 5 concurrent connections | [Start free](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Startup | 1,000,000 | $149 / $134.10 | 50 threads, US and EU geotargeting | [Get Startup](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Business | 3,000,000 | $299 / $269.10 | 100 threads, global country-level geotargeting | [Get Business](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Scaling | See pricing page | See pricing page | Pay-as-you-go, auto-upgrade | [Check Scaling](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Professional | See pricing page | See pricing page | Pay-as-you-go, auto-upgrade | [Check Professional](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Advanced | 21,500,000 (+500,000 bonus credits, limited offer) | $1,975 / $1,777.50 | 500 threads, priority routing, pay-as-you-go | [Get Advanced](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | Custom | Custom | Custom terms, pay-as-you-go | [Talk to sales](https://www.scraperapi.com/pricing?fp_ref=coupons) |

Three billing rules matter more than the headline numbers. Credits do not roll over; your balance resets when the subscription renews. Auto-upgrade (moving you to the next plan when credits run out) is opt-in and available on Hobby, Startup, Business, Scaling and Professional, but not on Advanced or Enterprise. Pay-as-you-go, which lets you keep scraping past your limit at a fixed per-credit rate up to a cap you set, is available on Scaling, Professional, Advanced and Enterprise only. If you expect spiky volume on Startup, budget for the upgrade rather than assuming you can overflow.

## What one credit actually buys

The credit table is where the real cost lives, and it is the part most comparisons skip. A plain page costs 1 credit. Amazon, Walmart and eBay cost **5 credits per request** because ScraperAPI maintains dedicated parsing for them. Google and Bing SERP requests cost 25, LinkedIn 30. Anything behind bot protection adds 10 credits for the bypass, JavaScript rendering adds 10, premium proxies add 10, and the two combined cost 25.

That turns into concrete page counts:

| Workload | Credits per request | What Startup's 1,000,000 credits buy |
| --- | --- | --- |
| Standard product page | 1 | 1,000,000 requests |
| Amazon / Walmart / eBay product page | 5 | 200,000 requests |
| Page behind Cloudflare | 11 (1 + 10 bypass) | ~90,900 requests |
| Page needing JS rendering and premium proxies | 25 | 40,000 requests |
| Google SERP | 25 | 40,000 requests |
| Ultra premium plus JS rendering | 75 | ~13,300 requests |

At 5 credits per Amazon page, Startup works out to about **$0.00075 per product page fetch**. Business lands near $0.0005 and Advanced near $0.00046, so the per-page price falls slowly as you scale up. Geotargeting, sessions, device type, output format and auto parsing are free and add nothing to the bill, which matters if you monitor the same product across several countries.

The estimator inside the dashboard gives the exact cost for any URL, and the `max_cost` parameter caps what a single request is allowed to spend. Use both before you commit to a plan size.

👉 [Check the current Startup price and credit allowance](https://www.scraperapi.com/pricing?fp_ref=coupons)

## Build versus buy: the honest cost comparison

Here is the calculation nobody puts in a comparison table. Pricefy's Pro plan costs $99/month (or $74 billed annually) and covers 2,000 SKUs with unlimited competitors and two price updates a day. Now price the same job on ScraperAPI, assuming three competitor URLs per product, fetched twice daily for 30 days: 2,000 × 3 × 2 × 30 = 360,000 requests. At 5 credits each, that is 1,800,000 credits, which puts you on **Business at $299/month**.

So the self-built route costs roughly three times the SaaS subscription before you have written a line of matching logic, a price history table, an alerting job, or a UI. That gap narrows if you already own those pieces, and it closes entirely if you were going to build them anyway. ScraperAPI is not the cheap option. It is the option where the data and the pipeline belong to you.

| Tool | Billing unit | Entry price | Repricing included? | Free tier |
| --- | --- | --- | --- | --- |
| ScraperAPI | API credits | $149/mo (1M credits) | No, you push prices back yourself | 1,000 credits, 5 concurrent connections |
| Pricefy | SKUs monitored | $49/mo, $37 billed annually | Dynamic repricing from Pro ($99/mo); autopilot and MAP/MSRP from Business ($189/mo) | 50 SKUs, 5 competitors, 1 update/day |
| Price Monitor | Not published | Not published | Yes, three strategies (underbid, rank target, match lowest) with floors and ceilings | Free account, no card required |
| UptimeRobot | Pages watched | Free | No | 50 pages, 5-minute checks |
| Price.com | Consumer alerts | Not published | No | Target-price alerts by email, text or push |

Price Monitor is the one worth a closer look if you sell on Amazon and eBay and want repricing without building it: it crawls those marketplaces plus Google Shopping, lets you configure underbid amounts, rank targets, shipping considerations and rounding rules per marketplace or per product, and exposes a REST API with keys for pushing data into an ERP. Its pricing is not published on the page I reviewed, so ask before you budget.

UptimeRobot deserves a mention for a different reason. Its free tier watches 50 pages, checks every five minutes, and emails you a before/after diff with a timestamp when the highlighted price element changes. If you are a buyer waiting for a laptop to drop, or a seller tracking a handful of competitor URLs by hand, that is enough, and buying any monitoring SaaS for that job is waste.

## The annual-versus-monthly trap

ScraperAPI's annual discount is a flat 10%: Startup drops from $149 to $134.10 a month, billed as $1,609.20 a year, saving $178.80. Business saves $358.80 a year, Advanced $2,370.

Pricefy displays the same kind of discount in a way that catches people out. The big number on each plan, $37, $74, $142, $374, is the monthly equivalent when you pay for a year up front. The struck-through numbers, $49, $99, $189 and $499, are what you pay month to month. Its own FAQ says paid plans start at $49/mo, which is correct and also not the number on the card. The Starter difference is $12 a month, or $144 a year. Worth knowing before you compare it to an API bill that quotes monthly rates.

ScraperAPI's annual plans can also renew early to get a fresh batch of credits, which is useful if you burn through an allowance before the period ends and don't want to change tiers.

👉 [Compare ScraperAPI monthly and annual pricing](https://www.scraperapi.com/pricing?fp_ref=coupons)

## What you have to build if you go the API route

ScraperAPI's documentation walks through a price monitoring job end to end, and reading it is the fastest way to see the real scope. Amazon and Walmart have structured endpoints that return JSON directly: for Amazon you get `pricing` (a formatted string like "$129.99" that you have to parse the number out of), `list_price`, `availability_status`, `product_information.title`, ratings and seller. Walmart returns `price`, `availability`, `seller_name` and `product_name`. Google Shopping returns a `shopping_results[]` array with `title`, `price`, `extracted_price`, `source` and `link`.

Those field names drift occasionally, so the advice in the official skill guide is to inspect the first real response of a run and adapt your parser. Four failure modes will bite you:

- **A 200 response with an empty price field** usually means the product is out of stock or the layout changed. Record it as null and surface it, don't treat it as a price of zero.
- **Currency has to travel with the number.** A reading of $1,299 is wrong if the listing was in CAD. Carry the currency code into every row.
- **Never compare across countries.** A baseline scraped with `country=us` and a current price with `country=gb` are different listings.
- **Status codes need different handling.** 401 means stop and fix the key. 403 means retry once with the premium flag, then mark the target failed. 404 means the product is gone. 429 means back off three seconds and retry once. 5xx gets up to three retries with 2/4/8-second backoff.

Then the boring parts. Batch jobs go through the Async endpoint, which returns a `statusUrl` per URL that you poll until the status reads finished, or you configure a destination bucket and a callback so results land in cloud storage without polling. Scheduling is a crontab entry, as the tutorial shows, running every day at 6am. Price history, change detection, alerting and writing new prices back to your store are all yours to build.

One shortcut worth taking: use the structured endpoints rather than scraping raw HTML when they exist. The parsing is the reason you are paying 5 credits instead of 1.

## Which setup fits your situation

**A few dozen pages, you just want to know when a price drops.** UptimeRobot's free tier handles 50 pages at five-minute intervals with zero setup. Don't buy anything.

**Under 100 SKUs, you sell on Shopify or WooCommerce, you want alerts in Slack.** Pricefy's Starter at $49/month ($37 billed annually) covers 100 SKUs, unlimited competitors and two daily updates. Its free plan covers 50 SKUs at one update a day if you want to test the matching quality first.

**You want prices changed automatically, not just watched.** On Pricefy that means Pro at $99/month for dynamic repricing with floors and ceilings; autopilot repricing and MAP/MSRP monitoring start at Business, $189/month. Below Pro you are getting data, not automation.

**Prices have to land in your own database, pricing engine or BI stack.** ScraperAPI, starting on Startup. Work out your monthly request count first: products × competitors × fetches per day × 30, then multiply by 5 for marketplace pages. If that lands under 200,000, Startup is enough. Between 200,000 and 600,000, Business. Above that, look at the mid-tiers and calculate per-credit cost rather than guessing.

**You monitor the same products across several countries.** Geotargeting is free on ScraperAPI and country-level targeting on Business covers the global case; Startup is limited to US and EU. Check that your target countries are inside your plan before you build the loop.

## Before you check out

Three things to settle first. Confirm the update frequency on the plan card, not the homepage: Pricefy's marketing says real-time while its plan table says one or two updates a day, and its FAQ says more frequent scraping is available for high-priority products. That is normal across this category, and the plan table is the number that governs what you get. Second, check whether a trial needs a card. Pricefy's free plan and Price Monitor's free account don't; ScraperAPI's 1,000-credit free tier is enough to run a few hundred Amazon pages through the parser and see the JSON before you pay anything. Third, note that ScraperAPI credits expire at renewal, so an annual plan sized for your worst month wastes money in the other eleven; size for the average and let pay-as-you-go absorb the peaks.

If the API route is the one that fits, start where the arithmetic points rather than where the sales page points.

👉 [Start on the ScraperAPI plan that matches your monthly page count](https://www.scraperapi.com/pricing?fp_ref=coupons)
