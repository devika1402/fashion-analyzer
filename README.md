# Fashion Trend Analytics with PySpark

Two analytical pipelines for fashion sales trend analysis, built with PySpark and Pandas/Matplotlib.

---

## What this does

The synthetic trend pipeline generates a two-year fashion dataset (10,000+ records across 9 categories, 10 styles, 13 colors, 4 seasons, and 5 regions) and runs aggregations to surface category revenue rankings, seasonal color performance, style popularity by social engagement, and regional preference patterns.

The Zara-style catalog pipeline builds a retail product catalog dataset with attributes typical of a fast-fashion retailer (category, style, color, price tier, stock status, bestseller flag) and runs category-level revenue analysis, seasonal color ranking, style-engagement cross-tabulation, and bestseller identification.

Both pipelines write structured JSON insights and multi-panel dashboards to the working directory.

---

## What the analysis surfaces

From the synthetic pipeline (10,000 records, 2-year window):

- Streetwear leads all styles at 806K units sold, 33% ahead of the lowest-performing style (Preppy, 606K units).
- White ranks as the top-selling color in 3 of 4 seasons. Navy dominates Summer.
- Regional preferences diverge across 5 markets: Minimalist leads in Asia and Europe, Streetwear in North America and Australia, Casual in South America.

From the Zara-style catalog:

- Outerwear generates the highest revenue ($995K) at an average price of $186. Tops generate $237K despite a comparable SKU count, showing how category price positioning drives revenue concentration.
- Wide Leg is the top-selling style by volume (5,110 units). Tailored leads in average social engagement (3,760 per item). High engagement does not predict high sales volume in this dataset.

---

## Requirements

**System**
- Python 3.8+
- Java 8 or 11 (required for PySpark)

**Python packages**

```
pip install pyspark pandas matplotlib seaborn requests beautifulsoup4
```

---

## Running

**Synthetic trend pipeline**

```
python fashion_analyzer.py
```

Outputs:
- `fashion_data.csv` - full synthetic dataset
- `fashion_insights.json` - aggregated findings
- `fashion_dashboard.png` - 6-panel dashboard
- `fashion_detailed_analysis.png` - monthly trend, heatmap, scatter, top combinations

**Zara-style catalog pipeline**

```
python zara_fashion_analyzer.py
```

Outputs:
- `zara_products.csv` - product catalog dataset
- `zara_insights.json` - aggregated findings (categories, seasonal colors, styles, bestsellers)
- `zara_dashboard.png` - catalog analytics dashboard
- `zara_detailed_analysis.png` - heatmap, scatter, stock status, top combinations

Note on live scraping: the Zara pipeline is structured to support extension to live data collection. The script runs on a generated dataset by default. Real scraping requires additional handling for rate limiting and anti-bot measures.

---

## Technical implementation

PySpark features used:
- DataFrame API for all transformations
- GroupBy aggregations: sum, avg, count
- Window functions (row_number over partitions) for seasonal top-N color ranking
- DataFrame caching for performance across multiple aggregation steps

Visualizations are produced via Pandas and Matplotlib/Seaborn, exported as PNG. JSON outputs are structured for direct downstream use.

Charts use a serif font stack (Sabon, falling back to Georgia and Times New Roman) with a light background style.
