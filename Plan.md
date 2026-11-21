# Pipeline Plan

## Source
- What: Crowdsourced food products prices from stores
- Where: Open Prices API (prices.openprices.org/api/v1/prices)
- Format: JSON, paginated list of price records
- Terms: Open Database License(ODBL), Credit Open Food Fasts


## Record Key
- One Record = one price observation
- key: id


## Data Contract ( What "valid" means)
- Required feilds : id, product, price, currency, date, location
- Type: int, object, number, string(Iso 4217), date, object 
- Rules:
    1. product is a valid object,
    2. price > 0,
    3. currency is valid ISO code
    4. date not in the future
    5. no duplicate id

## Layers
- Bronze: raw JSON page as received, plus fetched time and query params
- Silver: one typed row per price, username and images with other unwnted columns dropped
- Gold: median price per product per week, week-over-week % change, price outlier flag