# Google News API Complete Guide: Why Was It Shut Down, How to Scrape Google News Today, Which Tool Actually Works — and What's the Cheapest Way to Get Structured JSON Data?

So you just found out that the Google News API doesn't exist anymore. You went looking for an endpoint, maybe followed a Stack Overflow thread from five years ago, and ended up staring at a dead link. Happens to everyone.

Here's the short version of what happened and what you can actually do about it.

---

## What Happened to the Google News API?

Google deprecated its original News API back in 2011. The official reason was vague — something about focusing resources elsewhere — but the practical result was the same: developers who needed structured news data were left to figure it out themselves.

For a while, RSS feeds filled the gap. Google News still has RSS feeds, and for simple use cases they still work fine. But if you need clean JSON output, geotargeting, keyword filtering, real-time results at scale, or any kind of reliable data pipeline — RSS is not going to cut it.

That's where the modern alternatives come in.

---

## What Do People Actually Use the Google News API For?

Before jumping into solutions, it helps to be clear on what you're actually trying to build. The use cases for a Google News API span a pretty wide range:

- **Brand monitoring** — track when your company name, product, or executives appear in news coverage
- **Sentiment analysis** — feed extracted headlines and snippets into NLP pipelines to score media tone over time
- **Market research** — aggregate coverage by industry, geography, or topic to spot emerging trends
- **Financial intelligence** — pull earnings news, regulatory announcements, and market commentary
- **Lead generation** — monitor for funding rounds, executive moves, or product launches that signal buying intent
- **Competitive intelligence** — watch what's being written about your competitors in near real time

Each of these use cases has different requirements around freshness, volume, geographic scope, and output format. Keep yours in mind as you read through the options below.

---

## The Three Main Approaches to Accessing Google News Data

Since there's no official API, developers have converged on three approaches:

**1. Scraping APIs** — Send a URL or query to a managed proxy API that handles IP rotation, CAPTCHA bypassing, and JavaScript rendering, then returns raw HTML or structured JSON. You control what you scrape; the API handles the infrastructure.

**2. SERP APIs** — Services that specifically target search engine result pages and return structured data in clean JSON format. Some of these have dedicated Google News endpoints that give you titles, sources, publication dates, snippets, and article links without needing to parse HTML yourself.

**3. News aggregator APIs** — Third-party services like NewsData.io, GNews, or NewsCatcher that index news from their own crawlers. You query their database rather than hitting Google directly. Data freshness and source coverage varies by provider.

For most developers who specifically want Google News results — the same editorial ranking, the same freshness signals, the same sources Google shows — option 1 or 2 is the right path. You're accessing Google's own result pages, just through a tool that handles the blocking problem.

---

## ScraperAPI's Google News API Endpoint

ScraperAPI is one of the more widely used scraping API tools, and it has a dedicated Google News structured data endpoint worth knowing about.

The endpoint hits the Google News results page for any query and transforms the output into structured JSON — article titles, source names, publication dates, URLs, and snippets. You get the same results a user would see on Google News for that query, which means you benefit from Google's editorial freshness ranking automatically.

The API call is simple. In Python:

python
import requests

payload = {
    'api_key': 'YOUR_API_KEY',
    'query': 'artificial intelligence',
    'country_code': 'us'
}

response = requests.get(
    'https://api.scraperapi.com/structured/google/news',
    params=payload
)

news = response.json()


The same endpoint works with cURL, Node.js, PHP, Ruby, and Java. The `country_code` and `tld` parameters let you target specific Google News editions — useful if you're monitoring regional news or need data from non-US markets.

A few things worth noting:

- The structured data endpoints are available on **all plans, including the free tier** — you don't need a paid plan to test this
- Geotargeting beyond US/EU requires the Business plan ($299/mo) or higher
- Credits are consumed per request, and different request types have different credit costs

👉 [Try the Google News API endpoint free — get 1,000 credits on signup](https://www.scraperapi.com/?fp_ref=coupons)

---

## ScraperAPI Plans: Which One Makes Sense for Google News Scraping?

The credit math is the thing most people don't think about until it's too late. A basic HTML request costs 1 credit. JavaScript rendering adds 5 credits. Premium proxies or structured data endpoints cost more. This means your actual request volume per dollar is lower than the headline credit number suggests.

For Google News SERP scraping specifically, requests generally fall in the lower-to-mid credit range since you're hitting search result pages rather than heavily protected e-commerce sites.

Here's the current plan lineup:

| Plan | Monthly Price | API Credits | Concurrent Connections | Buy |
|------|--------------|-------------|------------------------|-----|
| Free | $0 | 1,000 | 5 |  [Get Free Plan](https://www.scraperapi.com/?fp_ref=coupons) |
| Hobby | $49/mo | 100,000 | 20 |  [Get Hobby Plan](https://www.scraperapi.com/?fp_ref=coupons) |
| Startup | $149/mo | 1,000,000 | 50 |  [Get Startup Plan](https://www.scraperapi.com/?fp_ref=coupons) |
| Business | $299/mo | 3,000,000 | 100 |  [Get Business Plan](https://www.scraperapi.com/?fp_ref=coupons) |
| Enterprise | Custom | Custom | Custom |  [Contact Sales](https://www.scraperapi.com/?fp_ref=coupons) |

Annual billing gets you a discount — the Hobby plan drops to roughly $44/mo when paid yearly. New users get a 7-day trial with 5,000 free requests, and there's a 7-day no-questions refund policy.

A practical way to think about this: if you're monitoring 500 queries per day (brand mentions, competitor names, industry topics), the Startup plan at 1M credits/month gives you room to run even with multi-credit requests. The Hobby plan at 100K credits works for lighter monitoring use cases or smaller research projects.

---

## Beyond the News Endpoint: What Else ScraperAPI Handles

The Google News endpoint is one piece of a broader platform. For developers building news data pipelines, a few other capabilities are relevant:

**Async Scraper Service** — For high-volume jobs where you don't need results immediately, async scraping lets you send batches of requests and collect results later. Useful for historical data collection or daily bulk pulls.

**DataPipeline** — A no-code visual tool for building and scheduling scraping jobs. If you want a recurring Google News feed for specific queries delivered to a webhook, folder, or email on a set schedule, DataPipeline handles this without writing any code.

**Structured Data Endpoints** — Beyond Google News, the same endpoint pattern works for Google SERP, Google Jobs, Google Shopping, and Google Maps. If your monitoring use case spans multiple data types (news coverage + organic search rankings, for example), you can consolidate to a single API.

**IP Pool & Anti-bot** — ScraperAPI runs a pool of 40+ million IPs across datacenter, residential, and mobile types across 50+ countries. The platform uses machine learning and statistical analysis to handle CAPTCHA and anti-bot measures automatically, claiming a 99.9% success rate for supported targets.

---

## How ScraperAPI Compares for Google News Specifically

An independent benchmark from May 2026 (Scrapeway) put ScraperAPI at a 63% overall success rate across 12 target sites, ranking third out of eight tested scraping APIs, with an average response time of 5.3 seconds and a cost of roughly $3.24 per 1,000 requests.

For Google News specifically — which is not among the most aggressively protected targets — performance tends to be higher than the cross-site average. Google's news pages are more scraping-friendly than, say, Cloudflare-protected e-commerce sites, which is where the average success rate gets dragged down.

The credit multiplier system is the main thing to understand before committing to a plan. If you're scraping Amazon product pages with JavaScript rendering and premium proxies, you'll burn credits fast. If you're primarily hitting Google News endpoints — structured data calls on a less-protected target — your effective cost per request is lower and credits go further.

One limitation worth noting: residential proxies and geotargeting beyond US and EU markets are restricted to the Business plan and above. If you need to monitor regional Google News editions (say, news.google.com.br or news.google.co.uk with local editorial ranking), you'll need the $299/mo Business tier at minimum.

---

## Practical Setup: Getting Google News Data in 5 Minutes

If you want to get up and running quickly, here's the actual flow:

1. **Sign up** for a free ScraperAPI account — you get 1,000 credits to test with, no card required initially

2. **Grab your API key** from the dashboard

3. **Send a test request** to the Google News endpoint:

bash
curl "https://api.scraperapi.com/structured/google/news?api_key=YOUR_KEY&query=OpenAI&country_code=us"


4. **Review the JSON output** — you'll get a structured response with news article objects containing titles, source names, publication times, URLs, and snippets

5. **Scale up** once you've confirmed the data format works for your use case

The whole thing takes about five minutes to test. The free tier is enough to validate whether the output format matches what your pipeline needs before spending anything.

👉 [Start for free — 1,000 credits, no card required](https://www.scraperapi.com/?fp_ref=coupons)

---

## Common Questions About Google News API Access

**Is it legal to scrape Google News?**

Google News aggregates publicly available articles. Scraping the metadata — titles, source names, URLs, publication dates, snippets — from search result pages is generally considered access to publicly available data. The legal picture around web scraping is nuanced and varies by jurisdiction and use case, so consulting a legal professional for production use is always the sensible move. Scraping APIs like ScraperAPI are designed to handle the technical challenges; the compliance question is separate and user-dependent.

**What's the difference between scraping Google News and using a news aggregator API?**

A news aggregator API (NewsData.io, GNews, NewsCatcher, etc.) gives you results from their own index. You're not hitting Google's servers at all — you're querying a third-party database. This is simpler and often cheaper for basic use cases, but you lose Google's editorial ranking signals, freshness ordering, and the coverage breadth of Google's crawler. If you specifically want what Google News shows for a query, you need to scrape Google News directly.

**Do Google News results vary by country?**

Yes, significantly. Google News has distinct editions by country and language, and the top stories for a query can be very different depending on which edition you access. ScraperAPI's `country_code` and `tld` parameters let you specify which Google News edition to query — useful for international brand monitoring or multilingual market research. Full geotargeting flexibility (beyond US and EU) is available on the Business plan.

**What happens when credits run out mid-month?**

On the standard plans (Hobby, Startup, Business), usage pauses when you hit your credit limit. As of early 2026, Enterprise and custom plans moved to a pay-as-you-go model with spending caps, so you can set a ceiling rather than having scraping stop abruptly. If you're running production workflows, the Business plan's 3M monthly credits and pay-as-you-go overflow options give you the most flexibility.

---

## The Bottom Line

The original Google News API is gone and has been for a long time. But the data is still there — accessible through scraping APIs that handle the proxy, CAPTCHA, and rendering problems so you don't have to.

ScraperAPI's dedicated Google News structured data endpoint is one of the more developer-friendly options: simple API call, clean JSON output, country targeting, available on all plans including free. For teams already using ScraperAPI for other data collection, adding Google News monitoring is a single endpoint away.

For new projects, the free tier is enough to test the data format and validate your pipeline. The Hobby plan at $49/mo covers most individual developer and small-scale research use cases. The Startup plan at $149/mo handles serious volume — a million credits a month covers a lot of news monitoring queries.

👉 [Create a free ScraperAPI account and test the Google News endpoint](https://www.scraperapi.com/?fp_ref=coupons)
