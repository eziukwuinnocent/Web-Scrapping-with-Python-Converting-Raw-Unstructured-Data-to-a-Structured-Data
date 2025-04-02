# Web Scrapping with Python: Converting Raw Unstructured Data to a Structured Data

![Image Alt](https://github.com/eziukwuinnocent/Web-Scrapping-with-Python-Converting-Raw-Unstructured-Data-to-a-Structured-Data/blob/e7fc0adc6e42573035978c4d46820fcc1c8b0558/british-airways.jpg)

This project involved a comprehensive collection of customer feedback data for British Airways (BA) from a third-party review platform. The objective was to extract raw unstructured web data, and transform it into structured (tabular) data for future analysis and to uncover insights into customers' sentiments regarding various aspects of their flight experiences. Leveraging web scraping techniques, I successfully gathered a substantial dataset of customer reviews from the web, focusing on key attributes such as customer review, satisfaction rating, date of flight booking, and destination country.

![Image Alt](https://github.com/eziukwuinnocent/Web-Scrapping-with-Python-Converting-Raw-Unstructured-Data-to-a-Structured-Data/blob/c5766b5a52d8924a17b7df4f931333ffc82f79c2/British_Airways_web_scrape.png)

# Steps and Code Interpretation [code executed with Spyder IDE version 5.15.10 | Python 3.11.7)

1. import pandas as pd

This line imports the pandas library, which is essential for data manipulation and analysis. It's aliased as pd for brevity, allowing you to refer to pandas functions using pd.function_name().

2. import numpy as np

This imports the numpy library, which provides support for numerical operations and arrays. It's aliased as np. While it isn't directly used in the provided code, it's often used in conjunction with pandas for data analysis.

3. from bs4 import BeautifulSoup

This line imports the BeautifulSoup class from the bs4 (Beautiful Soup 4) library. BeautifulSoup was used here for parsing documents, making it crucial for web scraping

4. import requests

This imports the requests library, which is used to make HTTP requests. In this case, it's used to fetch the HTML content of the web pages.

5-7. (Blank Lines)

These are empty lines for code readability.

8. reviews = []

This initializes an empty list called reviews. This list will store the text content of the customer reviews extracted from the web pages.

9. stars = []

This initializes an empty list called stars. This list will store the star ratings associated with each review.

10. date = []

This initializes an empty list called date. This list will store the dates when the reviews were posted.

11. country = []

This initializes an empty list called country. This list will store the country from which each review was posted.

13. for i in range(1, 36):

This starts a for loop that iterates through web page numbers from 1 to 35 (inclusive). This loop is used to scrape data from multiple pages of the website.

14. page = requests.get(f"https://www.airlinequality.com/airline-reviews/british-airways/page/{i}/?sortby=post_date%3ADesc&pagesize=100")

This line uses the requests.get() function to fetch the HTML content of each page. The f-string dynamically inserts the page number i into the URL. The URL is set to sort the reviews by date, descending, and to show 100 reviews per page.

16. soup = BeautifulSoup(page.content, "html.parser")

This line creates a BeautifulSoup object named soup. It parses the HTML content of the fetched page (page.content) using the "html.parser" parser.

18. for item in soup.find_all("div", class_="text_content"):

This starts a loop that iterates through all div elements with the class "text_content" found in the parsed HTML. These elements contain the text of the reviews.

19. reviews.append(item.text)

Inside the loop, this line extracts the text content of each review (item.text) and appends it to the reviews list.

21. for item in soup.find_all("div", class_ = "rating-10"):

This starts a loop that iterates through all div elements with the class "rating-10". These elements contain the star ratings.

22-26. try...except Block

This try...except block handles potential errors that might occur when extracting star ratings.

try:: attempts to extract the star rating.

stars.append(item.span.text): If successful, it appends the text of the span element (which contains the star rating) to the stars list.

except:: If an error occurs (e.g., if the span element is not found), it executes the code in the except block.

print(f"Error on page {i}"): prints an error message containing the page number.

stars.append("None"): appends the string "None" to the stars list to indicate a missing rating.

29-30. Date extraction

for item in soup.find_all("time"):: loops through all 'time' html elements on the page.

date.append(item.text): adds the text of the time element to the date list.

33-34. Country extraction

for item in soup.find_all("h3"):: loops through all h3 html elements on the page.

country.append(item.span.next_sibling.text.strip(" ()")): adds the next sibling of the span element within the h3 element to the country list, and also strips off any parenthesis and spaces.

37, 38, 40, 41. len(reviews), len(stars), len(date), len(country)

These lines print the lengths of the reviews, stars, date, and country lists, respectively. This is likely used to verify that the scraping process collected the expected number of items.

43. stars = stars[:3500]

This slices the stars list, keeping only the first 3500 elements. This is done to ensure the lists are the same length, since there can be issues with the amount of stars scraped.

44. print(stars)

This line prints the now modified stars list.

45-48. Pandas Series Creation

These lines create pandas Series objects from the reviews, stars, date, and country lists. Pandas Series are one-dimensional labeled arrays capable of holding any data type.

49-50. Pandas DataFrame Creation

df = pd.DataFrame({"reviews": reviews_series, "stars": stars_series, "date": date_series, "country": country_series})

This creates a pandas DataFrame named df from the previously created Series. A DataFrame is a two-dimensional table-like data structure.

51. print(df)

This line prints the DataFrame to the console.

53. BA_table = df.to_csv("BA.csv", index= True)

This line saves the DataFrame df to a CSV file named "BA.csv". The index=True argument includes the DataFrame's index (row numbers) in the CSV file.

54. print(BA_table)

This line will print none, as the to_csv function returns none.

This code effectively scrapes customer reviews, star ratings, dates, and countries from the specified website, cleans and organizes the data, and saves it to a CSV file.
