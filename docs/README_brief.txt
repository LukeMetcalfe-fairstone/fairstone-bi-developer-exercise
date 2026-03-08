BI Developer – Take‑Home Exercise (60 minutes)

**Scenario:** You’ve been given **staging‑layer style CSVs** representing clients, advisers, products and transactions. Your job is to propose a **reporting‑layer star schema** and demonstrate light transformation logic suitable for a governed reporting model.

> Focus on **data modelling decisions**, clear **fact/dimension design**, and concise **SQL/transform** examples. Reporting visuals are **not required**.

---

 Deliverables (place in `/submission`)

1. **`star_schema.md`** – A simple depiction of your proposed model. Show:
   - Fact table name and **grain** (e.g., `fact_adviser_revenue` at **transaction** grain)
   - Dimension tables and keys (e.g., `dim_client`, `dim_adviser`, `dim_product`, `dim_date`)
   - Join keys & surrogate keys where relevant
   - Any SCD assumptions (SCD1 vs SCD2)

2. **`sql_examples.sql`** – Up to **3 snippets** that demonstrate your approach, for example:
   - Building a dimension (e.g., `dim_adviser`) with a surrogate key and basic SCD handling
   - Building `fact_adviser_revenue` from `stg_transactions` (refund treatment, null handling, currency assumption)
   - Example join or KPI calc (e.g., monthly revenue by adviser band vs target)

3. **`approach.md`** (≤1 page) – Briefly explain:
   - Modelling decisions and trade‑offs (grain, keys, conformed dims)
   - Data quality issues noticed in the staging CSVs and suggested fixes / ownership
   - Where KPI logic should live (model vs semantic layer)
   - **If I had more time…** (what you would improve next)

Timebox: **~60 minutes**. It’s fine if you don’t finish everything – prioritise clarity over completeness.

---

 Data you are given (CSV files)
- `stg_clients.csv`
- `stg_advisers.csv`
- `stg_products.csv`
- `stg_transactions.csv`
- `stg_kpi_targets.csv`

> Staging data includes intentional issues to consider in your model: duplicate advisers, null foreign keys, mixed date formats, product family/name inconsistencies, refunds (negative values), potential SCD attributes (e.g., adviser region), and non‑atomic columns (e.g., `full_address`).

---

 Tools You May Use
You may use **any SQL or transformation environment** you are comfortable with:
- **SQL** (Postgres, SQL Server, MySQL, BigQuery, Snowflake, DuckDB, etc.)
- **Azure Databricks** (Community Edition) – SQL or PySpark
- **Python** (pandas or PySpark)
- **Power BI** (Power Query M, DAX)
- **Tableau Prep** (if preferred)

**Optional no‑install SQL:** DuckDB WASM (browser) – https://shell.duckdb.org

---

 Guidance (you may adapt with justification)
- **Revenue** = sum of `fee_amount` where `is_refund = 'N'` (or invert negatives accordingly).
- Consider a `dim_date` rather than embedding dates in facts.
- Resolve product hierarchy inconsistencies into a conformed `dim_product`.
- Treat adviser region changes as SCD1 or SCD2 (state your choice and why).
- Handle null/missing foreign keys (default/unknown members).
- Keep business keys stable; generate surrogate keys where appropriate.

---

 What “good” looks like
- Fact grain is explicit and defensible; dims are tidy and conformed.
- SQL snippets are clear, performant‑leaning and robust to dirty data.
- Sensible SCD strategy and unknown member handling.
- Clear communication and pragmatic trade‑offs in 60 minutes.