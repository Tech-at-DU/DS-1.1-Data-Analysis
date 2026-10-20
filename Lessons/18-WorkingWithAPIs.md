## Working with APIs & Real-World Data

### Learning Objectives
By the end of this lesson, students will be able to:
1. Make an HTTP GET request to a public API and parse the JSON response
2. Convert nested JSON into a flat pandas DataFrame
3. Handle common real-world API issues: pagination, rate limits, missing/optional fields
4. Explain why pulling live data differs from working with a static CSV

### Why APIs?

Every dataset so far in this course has been a static CSV, already cleaned and sitting in a folder. Real analyst work often starts differently — pulling live data from a web service. An **API** (Application Programming Interface) is how one program asks another for data over the internet. Most public data (weather, government stats, sports scores, prices) is available this way, and it's a fundamentally different shape of problem than reading a CSV: the data can change between requests, it might be paginated, and it arrives as **JSON**, not rows and columns.

### Making a Request

```python
import requests

response = requests.get('https://api.example.com/some-endpoint')
response.status_code   # 200 = success, 4xx = your request was wrong, 5xx = their server's problem
data = response.json() # parses the JSON response body into Python dicts/lists
```

Always check `response.status_code` (or call `response.raise_for_status()`) before trying to use the data — a failed request still returns *something*, and silently treating an error page as data is a common source of confusing bugs.

### JSON → DataFrame

JSON is naturally nested (dicts inside dicts, lists inside dicts), while a DataFrame is flat (rows and columns). `pd.json_normalize()` bridges the two:

```python
import pandas as pd

# Example: a typical nested API response shape
raw = {
    "results": [
        {"name": "Alice", "address": {"city": "Austin", "zip": "78701"}},
        {"name": "Bob", "address": {"city": "Reno", "zip": "89501"}},
    ]
}

df = pd.json_normalize(raw["results"])
# columns: name, address.city, address.zip
```

### Real-World API Issues

- **Pagination** — APIs rarely return everything in one response. You usually get a page of results plus either a `next` URL or a page number to request next, and you loop until there's no more data.
- **Rate limits** — most APIs cap how many requests you can make per minute/hour. Hitting the limit usually returns a `429 Too Many Requests` status. Space out requests (`time.sleep()`) if you're making many.
- **Missing/optional fields** — unlike a CSV with a fixed set of columns, not every JSON record has every field. Use `.get('field', default)` instead of `['field']` to avoid `KeyError` on records that omit it.
- **API keys** — many APIs require a key for authentication. **Never commit an API key to git** — read it from an environment variable or a local, git-ignored file instead.

### Check Your Understanding

Answers: [Solutions/WorkingWithAPIs.md](../Solutions/WorkingWithAPIs.md).

1. What does a `200` status code mean? What's the general difference between a `4xx` and a `5xx` response?
2. Why use `pd.json_normalize()` instead of just passing a raw nested dict straight into `pd.DataFrame()`?
3. Why check `response.status_code` before calling `response.json()`, instead of just calling `.json()` directly?

### Topics
- HTTP requests: `requests.get()`, status codes
- JSON structure and `pd.json_normalize()`
- Pagination and rate limits
- Handling missing fields safely
- API key hygiene

### Resources
- [requests: Quickstart](https://requests.readthedocs.io/en/latest/user/quickstart/)
- [pandas: `json_normalize`](https://pandas.pydata.org/docs/reference/api/pandas.json_normalize.html)
- [Public APIs (no key required) — a curated list](https://github.com/public-apis/public-apis)
- Complete the [companion notebook](../Notebooks/18-WorkingWithAPIs.ipynb)

### Challenges

Deliverable: a notebook that pulls live data from a public, no-key-required API, converts it to a DataFrame, and answers 4 questions about it.

This lesson uses the free [Open-Meteo](https://open-meteo.com/) weather API (no signup required) as the running example, but any no-key public API works for the challenges.

1. Request current weather for a city of your choice:
   `https://api.open-meteo.com/v1/forecast?latitude=30.27&longitude=-97.74&current=temperature_2m,wind_speed_10m` (these coordinates are Austin, TX — swap in your own)
2. Parse the JSON response and pull out the `current` section into a DataFrame (or a plain dict is fine for a single-record response — `pd.json_normalize` shines once you have a *list* of records)
3. Request a **7-day forecast** instead (add `&daily=temperature_2m_max,temperature_2m_min` to the URL) and convert the `daily` section — which contains a list of values per field — into a proper DataFrame with one row per day
4. Answer with code:
   - What's the highest forecasted max temperature in the next 7 days?
   - What's the average forecasted min temperature?
   - Plot the 7-day max/min temperature as a line chart

### Stretch Challenges
- Wrap your request in a function that checks `response.status_code` and raises a clear error message if the request failed
- Find a second no-key public API (see the list linked in Resources) and pull one dataset from it

### Self-Check

Weather data changes daily, so there's no fixed number to check your answer against here — instead, verify your *process*:

- [ ] My request checks `response.status_code` (or calls `.raise_for_status()`) before touching the response body
- [ ] My `current` weather data is a DataFrame or dict with named fields (`temperature_2m`, `wind_speed_10m`), not a raw unparsed JSON string
- [ ] My `daily` forecast is a DataFrame with **7 rows** (one per day) and columns for date, max temp, min temp — not one row with 7-item lists crammed into each cell
- [ ] "Highest forecasted max" and "average forecasted min" are each a single number, computed with pandas (`.max()`, `.mean()`), not read off the printout by eye
- [ ] My line chart has both max and min temperature, a legend, and readable date labels
- [ ] I got all 3 Check Your Understanding questions right (see [Solutions](../Solutions/WorkingWithAPIs.md))
- [ ] Stretch: my wrapped request function correctly detects and reports a failed request
