# search-api

An Azure Function (Python) that gives the portfolio's Safari window real Google results and Google Images.
It calls SerpApi, trims the response and returns it to the page, so the SerpApi key never reaches the browser.

## Endpoints

- `GET /api/search?q=python&type=web` returns web results, a knowledge card, an answer box,
  related questions and related searches.
- `GET /api/search?q=python&type=images` returns images; add `&page=1`, `&page=2` for more.

Results are cached for 10 minutes so repeated searches do not use SerpApi quota, and requests from any
origin other than `ALLOWED_ORIGIN` are refused. When the SerpApi quota runs out, the page falls back to
opening Google in a new tab.

## Configuration

Set these as application settings on the Function App:

- `SERPAPI_KEY`: the SerpApi key
- `ALLOWED_ORIGIN`: the portfolio's address; separate several with commas (add `http://localhost:8000` for local testing)

## Deploy and test

    func azure functionapp publish portfolio-search-fcayaag9fbeufpfd

    pip install azure-functions
    python test_function.py
