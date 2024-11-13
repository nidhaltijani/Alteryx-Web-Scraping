# US NASDAQ Stock Prices Web Scraping with Alteryx

This project is an Alteryx-based web scraping workflow that extracts US NASDAQ stock prices from CentralCharts. It captures data across 124 pages and performs data transformations to generate a structured dataset for analysis. The workflow is designed to handle various aspects of data extraction, cleaning, and export, using Alteryx's nodes and tools.

## Project Overview

- **Data Source**: [CentralCharts - US NASDAQ Stocks](https://www.centralcharts.com/en/price-list-ranking/ALL/asc/ts_19-us-nasdaq-stocks--qc_1-alphabetical-order?p=1)
- **Pages Scraped**: 124
- **Tools Used**: Alteryx Designer
- **Output**: A cleaned and structured CSV file (`Scraped_data.csv`) containing stock price data from the NASDAQ.

## Workflow Overview

![Alt Text](Screenshots/Full_workflow.jpg)

The Alteryx workflow is divided into the following sections:

1. **Page Cycling and URL Generation**  
2. **Web Scraping**
3. **Table Header Adjustment**
4. **Value Treatment**
5. **Data Export**

### Workflow Components

#### 1. Page Cycling and URL Generation
   - **Purpose**: This part of the workflow dynamically generates URLs for all 124 pages of stock data.
   - **Key Steps**:
     - The URL base template is concatenated with the page numbers, allowing the workflow to loop through each page.
     - An "If" condition checks if the URL field is empty, ensuring URLs are generated correctly for all pages.

#### 2. Web Scraping
   - **Purpose**: Extracts stock data from each page.
   - **Key Steps**:
     - The workflow fetches HTML content for each page URL.
     - A series of conditions and filters check for the presence of relevant data in the downloaded HTML (e.g., tables and specific tags).
     - A flag is set when relevant data is found, which enables further processing in the next steps.

#### 3. Table Header Treatment
   - **Purpose**: Ensures consistency in table headers across all pages, as HTML structures might vary.
   - **Key Steps**:
     - Replacement nodes are used to modify the headers as needed.
     - Conditions check if headers are empty and, if so, replace them with standard headers to maintain uniformity.

#### 4. Value Treatment
   - **Purpose**: Cleans and standardizes extracted data values.
   - **Key Steps**:
     - Replaces null values or placeholder strings with appropriate values.
     - Various parsing and transformation nodes format data columns to make them consistent.
     - Duplicate checks and null handling are applied to prepare the data for export.

#### 5. Data Export
   - **Purpose**: Writes the final cleaned data to a CSV file.
   - **Output**: The cleaned stock data is exported to `Scraped_data.csv`, ready for further analysis or visualization.

## Example Output

| URL | Financial Instrument | Current Price | Change(%) | Open | High | Low | Volume | Cap. | Issued Cap. |
|-----|-----------------------|---------------|-----------|------|------|------|--------|------|-------------|
| [CentralCharts Page 79](https://www.centralcharts.com/en/price-list-ranking/ALL/asc/ts_19-us-nasdaq-stocks--qc_1-alphabetical-order?p=79) | NICE LTD ADS | 192.07 | +1.09% | 191.10 | 192.79 | 188.61 | 584178 | - | - |
| [CentralCharts Page 79](https://www.centralcharts.com/en/price-list-ranking/ALL/asc/ts_19-us-nasdaq-stocks--qc_1-alphabetical-order?p=79) | NIKOLA CORP. | 3.25 | +7.62% | 3.02 | 3.35 | 2.96 | 4728170 | - | - |
| [CentralCharts Page 79](https://www.centralcharts.com/en/price-list-ranking/ALL/asc/ts_19-us-nasdaq-stocks--qc_1-alphabetical-order?p=79) | NIOCORP DEVELOPMENTS | 1.46 | -0.68% | 1.53 | 1.53 | 1.46 | 134884 | - | - |
| [CentralCharts Page 79](https://www.centralcharts.com/en/price-list-ranking/ALL/asc/ts_19-us-nasdaq-stocks--qc_1-alphabetical-order?p=79) | NIP GROUP INC. ADS | 6.22 | -4.31% | 6.50 | 6.55 | 6.22 | 109694 | - | - |
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

## How to Run the Workflow

1. Open the workflow file in Alteryx Designer.
2. Ensure your environment has access to the internet to fetch data from the source URL.
3. Run the workflow, which will scrape data across 124 pages, clean it, and export the result to `Scraped_data.csv`.

## Future Improvements

- **Error Handling**: Implement error handling for network failures.
- **Automated Scheduling**: Schedule the workflow to run periodically for updated data.
- **Additional Data Fields**: Scrape more detailed data if available on the source website.

## References

This project was inspired by the code and structure in the following GitHub repository:
- [Stock Web Scraper by bharding216](https://github.com/bharding216/stock-web-scraper/tree/main)
