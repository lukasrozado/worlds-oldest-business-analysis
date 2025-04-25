# World's Oldest Business Analysis 

# Quick Start

## Project Instructions

Understand the factors that help a business be timeless by answering these questions:

1. **What is the oldest business on each continent?**  
   Save your answer as a DataFrame called `oldest_business_continent` with four columns: `continent`, `country`, `business`, and `year_founded` in any order.

2. **How many countries per continent lack data on the oldest businesses? Does including `new_businesses` change this?**  
   Count the number of countries per continent missing business data, including `new_businesses`, and store the results in a DataFrame named `count_missing` with columns for the continent and the count.

3. **Which business categories are best suited to last many years, and on what continent are they?**  
   Create a DataFrame called `oldest_by_continent_category` that stores the oldest founding year for each continent and category combination. It should contain three columns: `continent`, `category`, and `year_founded`, in that order.

## Data Files

- `data/businesses.csv` and `data/new_businesses.csv`  
  - `business`: Name of the business (varchar)  
  - `year_founded`: Year the business was founded (int)  
  - `category_code`: Code for the business category (varchar)  
  - `country_code`: ISO 3166-1 three-letter country code (char)

- `data/countries.csv`  
  - `country_code`: ISO 3166-1 three-letter country code (varchar)  
  - `country`: Name of the country (varchar)  
  - `continent`: Name of the continent the country exists in (varchar)

- `data/categories.csv`  
  - `category_code`: Code for the business category (varchar)  
  - `category`: Description of the business category (varchar)

## Setup

```python
import pandas as pd

# Load the data
businesses = pd.read_csv("data/businesses.csv")
new_businesses = pd.read_csv("data/new_businesses.csv")
countries = pd.read_csv("data/countries.csv")
categories = pd.read_csv("data/categories.csv")
```

## Example Snippet

Below is an example for computing the oldest business by continent and category:

```python
# Merge and compute oldest by continent and category
category_merged = businesses.merge(categories, on="category_code", how="inner")
category_with_continent = category_merged.merge(countries, on="country_code", how="inner")
oldest_by_continent_category = (
    category_with_continent
    .groupby(["continent", "category"])
    .agg({"year_founded": "min"})
    .reset_index()
    .sort_values(["continent", "year_founded"])
)
print(oldest_by_continent_category)
```

**Staffelter Hof Winery** is Germany's oldest business, established in 862 under the Carolingian dynasty. It has served through dramatic historical changes—from the Holy Roman Empire and Ottoman Empire to both World Wars. What characteristics enable a business to stand the test of time?

This dataset from BusinessFinancing.co.uk covers the oldest company still in business for almost every country and has been cleaned. Use joining and data manipulation to bring all files together for your analysis.
