# Data Dictionary  
**Online Retail.csv** – source: UCI / Kaggle (CC0)

| Column | Data Type | Description | Example | Nulls |
|--------|-----------|-------------|---------|-------|
| InvoiceNo | string | 6-digit invoice identifier. Leading 'C' = cancelled order | 536365, C536391 | 0 % |
| StockCode | string | 5-digit SKU code (some alphanumeric) | 85123A | 0 % |
| Description | string | Product name | WHITE METAL LANTERN | 1.3 % |
| Quantity | integer | Units sold per line (**negative for returns**) | 6, -1 | 0 % |
| InvoiceDate | timestamp | Purchase moment (UK time) | 2011-01-12 08:26:00 | 0 % |
| UnitPrice | decimal(8,2) | Price per unit in £ | 3.39 | 0 % |
| CustomerID | integer | 5-digit customer key | 17850 | 25 % |
| Country | string | Customer’s billing country | United Kingdom | 0 % |

## Derived fields (created inside pipeline)
| Column | Derivation | Purpose |
|--------|------------|---------|
| Year, Month, Day, Week, DayOfWeek | `extract(date-part from InvoiceDate)` | calendar features |
| CountryIndex | `StringIndexer → cast(int)` | numeric country token |
| StockCodeIndex | `StringIndexer → cast(int)` | numeric SKU token |
| features | `VectorAssembler` | model input vector |
| prediction | `RandomForestRegressor` | forecast quantity (daily) |

## Cleaning choices
- Dropped rows with **negative Quantity** (returns) – keeps forecast positive-only.  
- Removed **missing CustomerID** – reduces leakage from one-time buyers.  
- Rolled to **daily granularity** – matches S&OP planning horizon.

## Target variable
- **Quantity** (daily sum) – integer ≥ 0 after cleaning.
