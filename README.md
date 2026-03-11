# SDS-hackathon-2026

## The "Safety First" Setup
Before you do anything, run this at the very top of your notebook. it keeps your laptop from freezing and sets the "speed limit."

`import os
import polars as pl`

## Prevents Polars from hogging every bit of CPU power
os.environ["POLARS_MAX_THREADS"] = "4"


## Don't "Read," just "Scan"
Never use pl.read_parquet(). You don't have enough RAM. Use scan_parquet() to create a LazyFrame. This acts as a "plan" rather than a "load."

This takes 0.001 seconds because it doesn't load the data yet
`df_lazy = pl.scan_parquet("data/aisdk-2024-1h.parquet")`


## Filter Early, Collect Late
The secret to working with "Big Data" on a small laptop is to throw away what you don't need before you bring it into memory.

Bad: Loading all 26 columns.

Good: Only selecting Latitude, Longitude, and MMSI.

# The "Go" Button
Your code will only actually run when you call .collect(). If it’s still slow, use streaming=True to process the data in small sips.

# The actual execution
`final_result = (
    df_lazy
    .filter(pl.col("Type of mobile") != "Base Station")
    .select(["MMSI", "Latitude", "Longitude"])
    .collect(streaming=True)
)`
