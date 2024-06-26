# Web_Scraping_in_python
Here's a formatted version of the README file for your GitHub repository:

---

# Wikipedia Table Scraper

This repository contains a Python script that scrapes tables from Wikipedia pages. The script uses the BeautifulSoup library for parsing HTML and the Requests library for making HTTP requests.

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Example](#example)

## Introduction

Wikipedia is a rich source of information, and sometimes you may need to extract data tables for analysis or other purposes. This project provides an easy-to-use script for scraping and processing tables from Wikipedia pages.

## Features

- Scrape any table from a Wikipedia page.
- Clean and preprocess the table data.
- Save the data to a CSV file for further analysis.

## Installation

To get started, you need to have Python installed on your machine. You can install the necessary packages using pip:

```bash
pip install beautifulsoup4 requests pandas
```

## Usage

To use the script, you need to specify the URL of the Wikipedia page and the index of the table you want to scrape.

```python
from bs4 import BeautifulSoup
import requests
import pandas as pd
url = "https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue"
page = requests.get(url)
soup = BeautifulSoup(page.text,'html')
table = soup.find('table',class_="wikitable sortable")
print(table)
world_titles = table.find_all("th")
world_titles
world_table_titles = [title.text.strip() for title in world_titles]
world_table_titles
df = pd.DataFrame(columns= world_table_titles)
df
column_data = table.find_all("tr")
column_data
for row in column_data[1:]:
    row_data = row.find_all("td")
    individual_row_data = [data.text.strip() for data in row_data] 
    print(individual_row_data)
    length= len(df)
    df.loc[length] = individual_row_data
df.to_csv(r'F:/Data Science Projects/python/web scraping/Compaines.csv',index=False)
```

### Command Line Usage

Alternatively, you can run the script from the command line:

```bash
python scrape_wikipedia_table.py <URL> <TABLE_INDEX>
```

## Example

Here's a complete example of scraping the first table from the Wikipedia page listing countries by GDP (nominal):

```python
for row in column_data[1:]:
    row_data = row.find_all("td")
    individual_row_data = [data.text.strip() for data in row_data] 
    print(individual_row_data)
    length= len(df)
    df.loc[length] = individual_row_data
df.to_csv(r'F:/Data Science Projects/python/web scraping/Compaines.csv',index=False)
```

This will save the scraped table to a file named `Compaines.csv`.

