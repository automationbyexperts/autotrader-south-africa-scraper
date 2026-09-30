# AutoTrader.co.za Scraper: South Africa Car Listings, Prices & Seller Phone Numbers

[![Run on Apify](https://img.shields.io/badge/Apify-Run%20the%20Actor-00A67E?logo=apify&logoColor=white)](https://apify.com/fayoussef/autotrader-co-za-scraper?fpr=youssef)
![Seller phone](https://img.shields.io/badge/Seller%20phone-captcha%20solved-2ea44f)
![Price](https://img.shields.io/badge/Price-ZAR-1C7ED6)
![Pagination](https://img.shields.io/badge/Pagination-every%20page-8B5CF6)
![Export](https://img.shields.io/badge/Export-JSON%20%7C%20CSV%20%7C%20Excel-F59E0B)

> ### ▶️ [Run the AutoTrader South Africa Scraper on Apify](https://apify.com/fayoussef/autotrader-co-za-scraper?fpr=youssef)
> Scrape **AutoTrader South Africa** car listings with ZAR price, mileage, specs, dealer rating, suburb and province, plus the **seller's phone number** that AutoTrader only shows after a captcha. No captcha account and no API key needed.

**AutoTrader South Africa Scraper** turns autotrader.co.za, South Africa's largest used car marketplace, into clean structured data: 25+ fields per vehicle across every result page. It is built for South African dealerships, bakkie and car traders, lead generation teams and automotive researchers. This repository documents the Apify Actor and gives working Python, JavaScript and cURL examples for calling it through the API.

- **Run it in the browser:** [fayoussef/autotrader-co-za-scraper on Apify](https://apify.com/fayoussef/autotrader-co-za-scraper?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/autotrader-co-za-scraper](https://automationbyexperts.com/apify/autotrader-co-za-scraper)
- **Actor ID for the API:** `fayoussef/autotrader-co-za-scraper`

## What the AutoTrader South Africa scraper does

- **Search pages**: paste any `autotrader.co.za/cars-for-sale` URL with your filters and every page is followed.
- **Whole dealer stock**: paste a dealer page and get that dealer's full inventory, or a dealer directory page (e.g. Johannesburg) and get every dealer in the city.
- **Single listings** are scraped on their own.
- **Seller phone numbers** (optional, paid plans): turn on **Scrape seller phone numbers** and every listing carries `phone_number`. The captcha is solved for you, once per dealer, and you only pay for numbers actually delivered.
- **Numeric ZAR prices and km mileage**, ready for spreadsheets.

## Output fields: what data you get

Each vehicle is one row with 25+ fields:

| Field | Description |
|---|---|
| `url` / `ad_id` / `status` | Listing link, ID, and Used, New or Demo |
| `make` / `model` / `variant` / `year` | Vehicle identity |
| `price_zar` / `price_str` | Price in rand, numeric and formatted |
| `mileage_km` / `mileage_str` | Mileage |
| `body_type` / `transmission` / `fuel_type` / `drivetrain` | Specs |
| `engine` / `engine_size` / `power_kw` / `torque_nm` | Engine and power |
| `exterior_colour` / `doors` | Body details |
| `phone_number` | Seller contact number (when phone scraping is on) |
| `dealer_name` / `dealer_id` / `dealer_rating_score` / `dealer_rating_count` | Dealer and its reviews |
| `seller_suburb` / `dealer_province` | Location |
| `image_urls` | Gallery photos |
| `description` | Full listing text |

## Input

Paste autotrader.co.za URLs and choose how much to scrape:

| Field | What it does |
|---|---|
| `start_urls` | Search, dealer, dealer directory or single listing URLs |
| `scrape_phone_numbers` | Add the seller phone number to every listing (paid plans) |
| `start_page` / `end_page` | Page range to scrape |
| `max_items` | Maximum number of listings |

## Use cases

- **Dealer and private seller lead lists** with phone numbers, by city or province.
- **Used car and bakkie pricing**: compare ZAR prices by make, model, year and mileage.
- **Competitor stock monitoring**: track a rival dealer's whole inventory on a schedule.
- **Car buying and trading**: find underpriced vehicles across South Africa.
- **Market research** on the South African used car market.

Ready-made examples you can run in one click:

- [Find used Toyota Hilux bakkies with seller phone numbers](https://apify.com/fayoussef/autotrader-co-za-scraper/examples/used-bakkies-with-seller-phone-numbers?fpr=youssef): Scrapes Toyota Hilux listings on AutoTrader South Africa and, on a paid plan, also returns the seller phone number AutoTrader hides behind a captcha, so the row is ready to call. Includes ZAR price, mileage, year, engine, dealer rating, suburb and province.

## Quick start

### 1. In the browser (no code)

1. Open the Actor on Apify and click **Try for free**.
2. Paste an autotrader.co.za search, dealer or listing URL into **Start URLs**, and turn on **Scrape seller phone numbers** if you need them.
3. Click **Start**, then download Excel, CSV or JSON from the **Output** tab.

### 2. Through the API

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

#### Python

```bash
pip install apify-client
python examples/python/run_actor.py
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fayoussef/autotrader-co-za-scraper").call(run_input={'start_urls': [{'url': 'https://www.autotrader.co.za/cars-for-sale/toyota/hilux'}],
 'scrape_phone_numbers': True,
 'max_items': 200})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

#### JavaScript / Node.js

```bash
npm install apify-client
node examples/javascript/run_actor.mjs
```

```javascript
import { ApifyClient } from "apify-client";

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor("fayoussef/autotrader-co-za-scraper").call({
    "start_urls": [
        {
            "url": "https://www.autotrader.co.za/cars-for-sale/toyota/hilux"
        }
    ],
    "scrape_phone_numbers": true,
    "max_items": 200
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

#### cURL (plain HTTP)

Runs the Actor and returns the dataset items in one synchronous call:

```bash
curl -X POST "https://api.apify.com/v2/acts/fayoussef~autotrader-co-za-scraper/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d @input.json
```

Synchronous calls time out after 300 seconds. For larger runs use the client libraries above, or start the run with `POST /v2/acts/fayoussef~autotrader-co-za-scraper/runs` and read the dataset when it finishes.

## Sample output

One record, from [`sample-output.json`](sample-output.json). Export the full dataset as JSON, CSV, Excel or HTML from the Apify Console, or read it through the API as shown above.

```json
{
  "url": "https://www.autotrader.co.za/car-for-sale/gwm/steed-5/2.0/28174398",
  "phone_number": "010 900 0000",
  "dealer_id": "389",
  "ad_id": 28174398,
  "year": 2025,
  "make": "GWM",
  "model": "Steed 5",
  "variant": "2.0VGT S",
  "status": "Used",
  "price_str": "R 294 900",
  "price_zar": 294900,
  "mileage_str": "12 000 km",
  "mileage_km": 12000,
  "transmission": "Manual",
  "fuel_type": "Diesel",
  "body_type": "Single cab",
  "exterior_colour": "White",
  "doors": 2,
  "engine": "2.0 turbo diesel",
  "engine_size": "2L",
  "power_kw": 110,
  "torque_nm": 320,
  "dealer_name": "GWM Haval The Glen",
  "seller_suburb": "Bassonia",
  "dealer_rating_score": 3.8,
  "dealer_rating_count": 32,
  "image_urls": [
    "https://img.autotrader.co.za/37182489/Crop800x600"
  ],
  "description": "Finance available through all major Banks. Trade in's welcome."
}
```

## Integrations and automation

- **Schedule it** daily to catch new listings and price changes from dealers you track.
- **Send results** to Google Sheets, Airtable, Slack, a webhook, Make, Zapier or n8n with Apify integrations.
- **Use it from AI agents** through the Apify MCP server.

## FAQ

### Does AutoTrader South Africa have an API?
No public one. This Actor is an AutoTrader.co.za API alternative: one Apify API call returns structured JSON for every listing.

### How do I get seller phone numbers from AutoTrader South Africa?
Turn on **Scrape seller phone numbers**. AutoTrader hides the number behind a captcha; the Actor solves it for you, with no captcha account or key. Phone numbers need an Apify paid plan.

### Why is phone scraping cheap on large runs?
A dealer's number is the same on every car it lists, so the captcha is solved once per dealer and reused. 500 cars from 40 dealers means 40 solves, not 500.

### Does it scrape all pages?
Yes. Pagination is followed automatically. Use `start_page`, `end_page` or `max_items` to scrape less.

### Can I filter by province, price or make?
Yes. Set the filters on autotrader.co.za, then paste the resulting URL into `start_urls`.

### Can I scrape a whole dealer inventory?
Yes. Paste the dealer page URL, or a dealer directory page to cover every dealer in a city.

### What output formats are available?
JSON, CSV, Excel, XML and HTML from the Apify dataset, or through the API.

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/autotrader-co-za-scraper?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## Related scrapers by AutomationByExperts

- [AutoTrader.ca Scraper: Canada Car Listings, VIN & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [AutoScout24 Scraper: European Car Listings & Dealer Phones](https://github.com/automationbyexperts/autoscout24-scraper)
- [Kijiji.ca Scraper: Cars, Rentals & Classifieds with Phones](https://github.com/automationbyexperts/kijiji-scraper)
- [CarGurus Scraper: US, Canada & UK Car Listings](https://github.com/automationbyexperts/cargurus-scraper)
- [Bulk AI Image Generator: Nano Banana & GPT Image](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner: ChatGPT, Claude & Gemini in Bulk](https://github.com/automationbyexperts/bulk-llm-runner)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/autotrader-co-za-scraper?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
