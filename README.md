# README — River Slope Analysis Using SWOT Node Data

## Overview

This script computes the linear slope statistics of river water surface elevation (WSE) profiles using SWOT-derived node elevation data, split into upstream and downstream segments based on the location of a known landslide initiation point.

It is designed to loop through multiple dates of input WSE data and outputs slope values in meters per kilometer (m/km), along with statistical indicators (standard error, confidence intervals, and p-values).

---

## Purpose

The goal is to quantify changes in river slope over time, particularly around a landslide site, by comparing WSE gradients upstream and downstream of a defined breakpoint.

---

## Input Data

* **Excel (.xlsx) files** containing SWOT node-derived WSE measurements.
* Each file must contain at least the following columns:

  * `X_UTM`: UTM coordinates along the river
  * `WSE`: Water Surface Elevation (meters)
  * `data_type`: Must include 'nodes'

Files are provided for the following observation dates:

```python
input_files = {
    "2024-07-12": "/content/WSE_nodes_2024-07-12.xlsx",
    "2024-08-13": "/content/WSE_nodes_2024-08-13.xlsx",
    "2024-09-08": "/content/WSE_nodes_2024-09-08.xlsx"
}
```
---

## Landslide Location

A fixed UTM coordinate (`x_break = 514305`) defines the landslide initiation point, used to separate:

* Upstream nodes (`X_UTM` < `x_break`)
* Downstream nodes (`X_UTM` ≥ `x_break`)

---

## Computed Outputs

For each date and each river segment (Upstream / Downstream), the script outputs:

* `Slope (m/km)`: Absolute value of the linear slope
* `Std Error (m/km)`: Standard error of the slope estimate
* `95% CI Lower / Upper (m/km)`: Lower and upper bounds of the 95% confidence interval
* `P-value`: Two-tailed p-value testing the null hypothesis that the slope = 0

Results are printed in tabular format to the console and stored as a `DataFrame` object (`results_df`).

---

## How It Works

1. **Load** node WSE data for each date
2. **Filter** to retain only valid node entries
3. **Split** into upstream and downstream based on the landslide coordinate
4. **Fit** a linear regression model to each segment
5. **Compute** slope-related statistics for each
6. **Print** all results in meters per kilometer (m/km)

---

## Requirements

* Python 3.x
* Libraries:

  * `pandas`
  * `numpy`
  * `scipy`
  * `os`

Install via:

```bash
pip install pandas numpy scipy
```
---
