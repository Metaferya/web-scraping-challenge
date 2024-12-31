# Mars News and Weather Data Analysis
## Overview
This repository contains two main deliverables that focus on web scraping and data analysis of Mars-related news and weather data. The projects use Python, Splinter, BeautifulSoup, Pandas, and Matplotlib to achieve the tasks.

## Deliverable 1: Scrape Titles and Preview Text from Mars News
## Objective
+ Scrape the titles and preview text of news articles from the Mars news site.

### Steps
1-Import Libraries: Import Splinter and BeautifulSoup.
from splinter import Browser
from bs4 import BeautifulSoup
2-Initialize the Browser: Use Splinter to initialize the browser.
browser = Browser('chrome')
3-Visit the Mars News Site: Navigate to the Mars news site.
url = 'https://static.bc-edx.com/data/web/mars_news/index.html'
browser.visit(url)
4-Scrape the Website: Create a Beautiful Soup object and extract text elements
html = browser.html
soup = BeautifulSoup(html, 'html.parser')
articles = soup.find_all('div', class_='list_text')
5-Store the Results: Extract titles and preview text and store them in a list of dictionaries.
mars_news = []
for article in articles:
    title = article.find('div', class_='content_title').text
    preview = article.find('div', class_='article_teaser_body').text
    news_dict = {'title': title, 'preview': preview}
    mars_news.append(news_dict)
print(mars_news)
6-Quit the Browser: Close the browser.
browser.quit()

## Deliverable 2: Scrape and Analyze Mars Weather Data
## Objective
+ Scrape and analyze Mars weather data from a Mars Temperature Data site.

#### Steps
1-Import Libraries: Import Splinter, BeautifulSoup, Matplotlib, and Pandas.
from splinter import Browser
from bs4 import BeautifulSoup
import matplotlib.pyplot as plt
import pandas as pd
2-Initialize the Browser: Use Splinter to initialize the browser.
browser = Browser('chrome')
3-Visit the Mars Temperature Data Site: Navigate to the Mars Temperature Data site.
url = "https://static.bc-edx.com/data/web/mars_facts/temperature.html"
browser.visit(url)
4-Scrape the Table: Create a Beautiful Soup object and extract the table data.
html = browser.html
soup = BeautifulSoup(html, 'html.parser')
table = soup.find('table')
rows = table.find_all('tr')
data = []
for row in rows[1:]:
    cols = row.find_all('td')
    cols = [col.text.strip() for col in cols]
    data.append(cols)
5-Store the Data: Assemble the scraped data into a Pandas DataFrame.
columns = ['id', 'terrestrial_date', 'sol', 'ls', 'month', 'min_temp', 'pressure']
mars_df = pd.DataFrame(data, columns=columns)
print(mars_df.head())
6-Prepare Data for Analysis: Examine and cast the data types.
mars_df['terrestrial_date'] = pd.to_datetime(mars_df['terrestrial_date'])
mars_df['sol'] = mars_df['sol'].astype(int)
mars_df['ls'] = mars_df['ls'].astype(int)
mars_df['month'] = mars_df['month'].astype(int)
mars_df['min_temp'] = mars_df['min_temp'].astype(float)
mars_df['pressure'] = mars_df['pressure'].astype(float)
print(mars_df.dtypes)
7-Analyze the Data: Use Pandas functions to answer key questions and plot results.
8-Save the Data: Export the DataFrame to a CSV file.
mars_df.to_csv('data/mars_weather.csv', index=False)
9-Quit the Browser: Close the browser.
browser.quit()

## Conclusion
This project demonstrates the use of web scraping and data analysis techniques to gather and analyze Mars-related data. The results provide insights into Mars' climate and weather patterns, enhancing our understanding of the Red Planet.

## Acknowledgments
Instructor: Thank you for providing valuable guidance and support throughout this project.

Xpert: Special thanks to Microsoft Copilot for assistance in coding and troubleshooting.



