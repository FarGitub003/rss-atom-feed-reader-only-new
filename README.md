# RSS & Atom Feed Reader – JSON, Only New Items

Turn RSS, Atom and JSON feeds into clean JSON. Scheduled, it delivers only the items it has never delivered before. Keyword filters, feed discovery from any page.

**▶ Run it on Apify Store: https://apify.com/far003/rss-atom-feed-reader-only-new**

> This repository hosts documentation and examples; the Actor runs on the Apify platform.

## What it does

- Reads any list of feeds (RSS 2.0, RSS 1.0, Atom and JSON Feed) and returns one clean JSON record per item: title, link, dates in ISO 8601, author, plain-text summary, full content, categories, enclosures, image.
- Give it a normal web page and it reads the feed the page declares.
- Scheduled, it delivers only the items it has never delivered before (the memory is kept per feed and per monitor name).
- Keyword include/exclude filters, maximum item age, and conditional requests (`ETag` / `Last-Modified`); one request per second per host.
- No proxies and no disguise: a feed that answers 403 or 429 to automated clients is reported as an error.

## Who it is for

- Slack, Telegram or email alerts with only the new posts.
- News or blog aggregators.
- Podcast and video-channel monitoring.
- Developers who want clean JSON instead of parsing feeds themselves.

## Example input

```json
{
  "feedUrls": ["https://blog.apify.com/rss/", "https://hnrss.org/frontpage"],
  "maxItemsPerFeed": 20
}
```

## Example output

```json
{
  "itemId": "6a841aaa343bc200019df9e6",
  "title": "Martina Gelnerová: from travel agency to data analyst",
  "link": "https://blog.apify.com/martina-gelnerova-data-career-change/",
  "publishedAt": "2026-10-01T08:46:24.000Z",
  "updatedAt": null,
  "author": "Nathanael Durham",
  "authors": ["Nathanael Durham"],
  "summary": "Apify mentors a team at every Czechitas Digital Academy. Martina Gelnerová was one of those students, and now she mentors there herself. …",
  "contentText": "Martina Gelnerová spent twenty years at a travel agency, pricing packages, and she loved it. \"I was so satisfied with the job there,\" she says.\nThen COVID arriv …",
  "contentHtml": "<img src=\"https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/2026/10/travel-agency-to- …",
  "categories": ["Life at Apify"],
  "enclosures": [],
  "image": "https://storage.ghost.io/c/f2/6e/f26ec999-9a90-4aee-a0d4-9b3ca2bb668f/content/images/2026/10/travel-agency-to-data-analyst.png",
  "commentsUrl": null,
  "language": null,
  "durationSeconds": null,
  "episode": null,
  "season": null,
  "explicit": null,
  "feedUrl": "https://blog.apify.com/rss/",
  "feedTitle": "Apify Blog",
  "feedLink": "https://blog.apify.com/",
  "feedType": "rss2",
  "fetchedAt": "2026-10-07T11:48:02.894Z",
  "isNew": true,
  "firstSeenAt": "2026-10-07T11:48:02.894Z"
}
```

## Use it from code

Set your token in the `APIFY_TOKEN` environment variable.

**Node.js** ([`apify-client`](https://docs.apify.com/api/client/js/))

```js
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('far003/rss-atom-feed-reader-only-new').call({
    "feedUrls": [
        "https://blog.apify.com/rss/",
        "https://hnrss.org/frontpage"
    ],
    "maxItemsPerFeed": 20
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

**Python** ([`apify-client`](https://docs.apify.com/api/client/python/))

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("far003/rss-atom-feed-reader-only-new").call(run_input={
    "feedUrls": ["https://blog.apify.com/rss/", "https://hnrss.org/frontpage"],
    "maxItemsPerFeed": 20
})
items = client.dataset(run["defaultDatasetId"]).list_items().items
print(items)
```

## Pricing

Pay per result — see the current price on the Store page.

## Data source & licence

The data is the content of the feeds you provide; it belongs to the publishers of those feeds. The Actor identifies itself as `FeedReaderBot`, uses conditional requests, spaces its requests, and refuses private and loopback addresses. You remain responsible for how you reuse the content of the feeds you read.

## Support

Open an issue in this repository or use the Issues tab on the Store page.

## Licence

The documentation and examples in this repository are released under the MIT licence (see `LICENSE`). The Actor itself is proprietary and runs on the Apify platform.
