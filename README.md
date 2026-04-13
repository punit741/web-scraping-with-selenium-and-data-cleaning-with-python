[README (2).md](https://github.com/user-attachments/files/26669204/README.2.md)
# 99Acres.com Web Scraper

A beginner-friendly web scraping project that collects real estate property listings from [99acres.com](https://www.99acres.com) for Delhi using Python and Selenium.

---

## Result

| Stage | Rows | Columns |
|---|---|---|
| Raw scraped data | 1521 | 5 |
| After cleaning | 1372 | 9 |

- 149 rows removed during cleaning (duplicates and unusable rows)
- 4 new columns added during cleaning

---

## What This Project Does

- Opens 99acres.com in a Chrome browser automatically
- Searches for properties in Delhi
- Applies filters: Verified, Ready to Move, With Photos, With Videos
- Goes through all result pages and collects property data
- Cleans the raw scraped data (removes duplicates, converts strings to numbers)
- Exports the final data as a CSV file

---

## Raw Data Sample

This is what the data looks like right after scraping, before any cleaning:

| name | location | price | area | bhk |
|---|---|---|---|---|
| Duplex of Basement & Ground | 5 BHK Builder Floor in Greater Kailash 2, Delhi | Rs.27 Cr | 5,000 sqft | 5 BHK |
| Vasant Vihar, Delhi, South Delhi | 4 BHK Builder Floor in Vasant Vihar, Delhi | Rs.16 Cr | 3,375 sqft | 4 BHK |
| Godrej South Estate\n4.0 | 2 BHK Flat in Okhla, Delhi | Rs.5.1 Cr | 1,442 sqft | 2 BHK |
| GREATER KAILASH | 2 BHK Builder Floor in Greater Kailash 2, Delhi | Rs.7 Cr | 2,300 sqft | 2 BHK |
| Govind Puri, Delhi, South Delhi | 2 BHK Builder Floor in Govind Puri, Delhi | Rs.37 Lac | 579 sqft | 2 BHK |

**Raw data had 0 null values** — all 1521 rows had complete data.

---

## Data Collected (Final Columns)

| Column | Description | Example |
|---|---|---|
| name | Property or society name | Godrej South Estate |
| location | Property type and area | 2 BHK Flat in Okhla, Delhi |
| price | Raw price text as scraped | Rs.5.1 Cr |
| area | Raw area text as scraped | 1,442 sqft |
| bhk | Raw BHK text as scraped | 2 BHK |
| price_cr | Price converted to Crore (float) | 5.1 |
| area_sqft | Area converted to number | 1442.0 |
| bhk_count | BHK as a number | 2.0 |
| price_per_sqft | Price divided by area (Rs. per sqft) | 35368.0 |

---

## BHK Distribution (after cleaning)

| BHK Type | Count |
|---|---|
| 3 BHK | 518 |
| 4 BHK | 748 |
| 5 BHK | 29 |
| 6 BHK | 9 |
| 7 BHK | 1 |
| 8 BHK | 2 |
| 18 BHK | 1 |

---

## Technologies Used

- Python 3
- Selenium — to control the Chrome browser
- Pandas — to store and clean the data
- NumPy — to handle missing values
- re (regex) — to extract numbers from text strings

---

## How to Run

**1. Install the required libraries**

```
pip install selenium pandas numpy
```

**2. Make sure you have Chrome installed and download ChromeDriver**

ChromeDriver version must match your Chrome browser version.
Download from: https://chromedriver.chromium.org/downloads

**3. Open the notebook**

```
jupyter notebook 99acres_webscraping.ipynb
```

**4. Run all cells from top to bottom**

The browser will open automatically and start scraping. When it finishes, a file called `99acres_delhi_properties.csv` will be saved in the same folder.

---

## Project Structure

```
99acres-scraper/
|
|-- 99acres_webscraping.ipynb       # main notebook
|-- 99acres_delhi_properties.csv    # output CSV (generated after running)
|-- README.md                       # this file
```

---

## Data Cleaning Steps

The raw scraped data has some issues that need to be fixed before analysis:

1. Remove duplicate rows
2. Fix property names — removes rating text like `\n4.0` that gets attached to the name
3. Convert price string to a float in Crore (handles both `Cr` and `Lac` units)
4. Convert area string to a float in sqft
5. Extract BHK number from text like `3 BHK` to `3.0`
6. Add a `price_per_sqft` column
7. Drop rows where all numeric columns are missing

---

## Notes

- The XPaths used for filter buttons are based on the 99acres layout at the time of scraping and may need updating if the site changes its structure.
- All `time.sleep()` values are kept reasonable to avoid getting blocked.
- Scraping was done for educational purposes only.

---

## Author

Made by a beginner learning web scraping with Python and Selenium.
