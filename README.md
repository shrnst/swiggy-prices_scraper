# Swiggy Prices Scraping Project

This script automates the process of scraping food item prices from Swiggy based on restaurant information provided in an Excel file.

## How It Works

1. **Prepare Excel File:**
   - Create an Excel file named "Sample.xlsx" with columns "Restaurant Name," "City," and "Zone" containing the restaurant information.

2. **Selenium and WebDriver:**
   - The script utilizes the Selenium library along with a Chrome WebDriver to automate the web browser.
   - A headless browser is used to simulate user interaction without a visible browser window.

3. **Google Search:**
   - For each restaurant in the Excel file, a Google search query is constructed by combining the restaurant name, city, and zone along with the keyword "Swiggy."
   - The script then navigates to Google and performs the search to find the Swiggy link associated with the restaurant.

4. **Selecting Swiggy Link:**
   - After the search results load, the script clicks on the Swiggy link to access the restaurant's Swiggy page.

5. **Scraping Prices with BeautifulSoup:**
   - Once on the Swiggy page, the script uses BeautifulSoup to scrape the names and prices of food items.
   - XPath is employed to locate the HTML elements containing the food item names and their associated prices.

6. **Random Selection:**
   - A random food item within a specified range is selected to add an element of randomness to the scraped data.

7. **Updating Excel File:**
   - The selected food item and its corresponding price are added to the original Excel file under new columns named "Food Item" and "Swiggy Prices."

8. **Random Delays:**
   - To mimic human behavior and avoid detection, the script introduces random delays between 1 and 3 seconds at various steps.

9. **Output:**
   - The updated data, including food item names and Swiggy prices, is saved in a new Excel file named "output_swiggy_data.xlsx."

## Dependencies

- `pandas`
- `selenium`
- `beautifulsoup4`
