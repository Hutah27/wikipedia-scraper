# Wikipedia Scraper for Past Elections

## Table of Contents

1. [Description](#description)
2. [Features](#features)
3. [Usage](#usage)
4. [Author](#author)

## 1. Description
This Python script scrapes election data from Wikipedia pages related to past elections and saves it to Excel files. It uses web scraping techniques with the `requests`, `BeautifulSoup`, and `openpyxl` libraries to fetch and process data from Wikipedia pages.

## 2. Features
- Scrapes data for past election results, including information on election types, districts, parties, candidates, votes, percentages, and links to candidate Wikipedia pages.
- Organizes the scraped data into Excel files for easy access and analysis.

## 3. Usage

### 3.1. Install Dependencies
If you haven't already, install the required Python libraries using pip:

```pip install requests```
```pip install beautifulsoup4```
```pip install openpyxl```

### 3.2. Run the Script

Download the script and execute it using Python:
```python past-scraper-one.py``` or ```past-scraper-two.py```

### 3.3. Provide Wikipedia Page Names
Follow the on-screen instructions to provide a list of Wikipedia page names (e.g., 2020 United States presidential election). Type 'done' in a new line when you've finished entering page names.

### 3.4. Data Extraction
The script will scrape candidate data and create separate Excel files for each Wikipedia page. These files will be saved in the same directory as the script and named after the Wikipedia page names.

### 3.5. Access Data
You can access the scraped election data in the generated Excel files. The data is organized in rows and columns for easy analysis.

## 4. Author
+ Author: Gurwinder Singh
+ Version: 1.0
+ Contact Author: For any issues or inquiries, please get in touch with the author on Upwork: [Author's Upwork Profile](https://upwork.com/freelancers/~0162de9053b9e180f4)
