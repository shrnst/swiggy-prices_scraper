
import pandas as pd
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
from bs4 import BeautifulSoup
import random
import time

# Load the Excel file
excel_file = "Sample.xlsx"
df = pd.read_excel(excel_file)

# Initialize the Chrome WebDriver
driver = webdriver.Chrome()

# Loop through each row in the Excel file
for index, row in df.iterrows():
    restaurant_name = row["Restaurant Name"]
    city = row["City"]
    zone = row["Zone"]

    # Construct the Google search query
    search_query = f"{restaurant_name} {city} {zone} Swiggy"
    driver.get("https://www.google.com")
    search_box = driver.find_element(By.NAME, "q")
    search_box.send_keys(search_query)
    search_box.send_keys(Keys.RETURN)

    # Wait for the results to load
    time.sleep(random.uniform(1, 3))

    # Find and click on the Swiggy link
    swiggy_link = driver.find_element(By.PARTIAL_LINK_TEXT, "Swiggy")
    swiggy_link.click()

    # Wait for the Swiggy page to load
    time.sleep(random.uniform(1, 3))

    # Scrape data from the page using BeautifulSoup
    soup = BeautifulSoup(driver.page_source, 'html.parser')

    # Find all the food items and their associated prices using XPath
    food_items = []
    swiggy_prices = []

    xpath_pattern = "/html/body/div/div[1]/div/div/div/div[2]/div[5]/div[1]/div/div[1]/div[1]/div/div[1]/div[2]/h3"
    for i in range(5, 15):  # Adjust the range as needed
        xpath = xpath_pattern.replace("div[5]", f"div[{i}]")
        try:
            item = driver.find_element(By.XPATH, xpath)
            food_item = item.text.strip()
            price_xpath = xpath.replace("div[2]/h3", "div[3]/span/span")
            price_element = driver.find_element(By.XPATH, price_xpath)
            price = price_element.text.strip()

            food_items.append(food_item)
            swiggy_prices.append(price)
        except:
            # Handle the case where the element is not found
            food_items.append("Not Found")
            swiggy_prices.append("Not Found")

    # Check if data was found
    if food_items:
        # Randomly select an item within the specified range
        num_items = len(food_items)
        random_index = random.randint(int(num_items * 0.05), int(num_items * 0.1))

        selected_food_item = food_items[random_index]
        selected_price = swiggy_prices[random_index]

        # Add the selected data to the DataFrame
        df.at[index, "Food Item"] = selected_food_item
        df.at[index, "Swiggy Prices"] = selected_price

    # Add a random delay between 1 and 3 seconds
    time.sleep(random.uniform(1, 3))

# Save the updated DataFrame to a new Excel file
output_excel_file = "updated_file.xlsx"
df.to_excel(output_excel_file, index=False)

# Close the WebDriver
driver.quit()
