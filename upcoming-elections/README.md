# Wikipedia Scraper for Upcoming Elections

## Table of Contents

1. [Description](#description)
2. [Features](#features)
3. [Usage](#usage)
4. [Author](#author)

## 1. Description
This script scrapes candidate data from Wikipedia pages related to upcoming elections and saves it to an Excel file. It is a Python script that uses the `requests`, `BeautifulSoup`, and `openpyxl` libraries to fetch and process data from Wikipedia pages.

## 2. Features
- Scrapes data for candidates participating in upcoming elections.
- Extract information such as election names, election links, districts, parties, candidate names, short descriptions, statuses, and links to candidate Wikipedia pages.
- Organizes data into an Excel file for easy access.

## 3. Usage

### 3.1. Install Dependencies
If you haven't already, install the required Python libraries using pip:

```pip install requests```
```pip install beautifulsoup4```
```pip install openpyxl```

### 3.2. Run the Script
Download the script and execute it using Python:
```python upcoming-scraper.py```

### 3.3. Provide Wikipedia Page Names
Follow the on-screen instructions to provide a list of Wikipedia page names (e.g. 2024 United States House of Representatives elections in Michigan). Type 'done' when finished.

### 3.4. Data Extraction
The script will scrape candidate data and create Excel files for each Wikipedia page. The files will be saved in the same directory where the script exists and named after the Wikipedia page names.

### 3.5. Access Data
The generated Excel files will contain candidate data organized in rows and columns.

## 4. Author
+ Author: Gurwinder Singh
+ Version: 1.0
+ Contact Author: For any issues or inquiries, please get in touch with the author on Upwork: [Author's Upwork Profile](https://upwork.com/freelancers/~0162de9053b9e180f4)
