# autotrader.co.za Car Scraper with Seller Phone Numbers

Scrape autotrader.co.za car listings across every page: price, mileage, specs, dealer and location, plus the seller's phone number.

This repo shows how to call the [autotrader.co.za Car Scraper with Seller Phone Numbers](https://apify.com/fayoussef/autotrader-co-za-scraper?fpr=youssef) Apify Actor from your own code: a Python and a JavaScript example, the input they send, and a sample of the output. Everything runs in the Apify cloud, so there is nothing to host, scale or maintain on your side.

- **Run it in the browser:** [fayoussef/autotrader-co-za-scraper on Apify](https://apify.com/fayoussef/autotrader-co-za-scraper?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/autotrader-co-za-scraper](https://automationbyexperts.com/apify/autotrader-co-za-scraper)
- **Actor ID for the API:** `fayoussef/autotrader-co-za-scraper`

## Use cases

- [Find used Toyota Hilux bakkies with seller phone numbers](https://apify.com/fayoussef/autotrader-co-za-scraper/examples/used-bakkies-with-seller-phone-numbers?fpr=youssef): Scrapes Toyota Hilux listings on AutoTrader South Africa and, on a paid plan, also returns the seller phone number AutoTrader hides behind a captcha, so the row is ready to call. Includes ZAR price, mileage, year, engine, dealer rating, suburb and province.
- [Export nearly new automatic cars for sale in South Africa](https://apify.com/fayoussef/autotrader-co-za-scraper/examples/nearly-new-automatic-cars-south-africa?fpr=youssef): Returns 2023 and newer automatic cars listed on AutoTrader.co.za with price, mileage, engine and power figures, dealer rating, location and gallery images. Useful for dealers sizing the late model market and for buyers comparing across provinces.

## Quick start

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

### Python

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

### JavaScript / Node.js

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

### cURL (plain HTTP)

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

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/autotrader-co-za-scraper?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## More Actors by AutomationByExperts

- [AutoTrader Canada Car Scraper: Prices, VIN, Mileage & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [AutoScout24 All-Country Scraper](https://github.com/automationbyexperts/autoscout24-scraper)
- [Kijiji.ca Scraper: Autos, Real Estate & Classifieds](https://github.com/automationbyexperts/kijiji-scraper)
- [CarGurus Scraper (US, Canada & UK Car Listings)](https://github.com/automationbyexperts/cargurus-scraper)
- [Bulk AI Image Generator (NO API KEY)](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner GPT, Claude, Perplexity, Kimi (No API Key)](https://github.com/automationbyexperts/bulk-llm-runner)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/autotrader-co-za-scraper?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
