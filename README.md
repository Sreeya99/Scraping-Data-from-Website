# Scraping-Data-from-Website
#using python

from bs4 import BeautifulSoup
import requests
url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'
page = requests.get(url)
Soup = BeautifulSoup(page.text,'html')
print(Soup)
table = Soup.find_all('table')[1]
print(table)
world_tittles = table.find_all('th')
world_tittles
world_table_tittles =[tittle.text.strip() for tittle in world_tittles]
print(world_table_tittles)
import pandas as pd
df = pd.DataFrame(columns = world_table_tittles)
df
column_data = table.find_all('tr')
for row in column_data[1:]:
    row_data = row.find_all('td')
    individual_row_data = [data.text.strip() for data in row_data]
    length = len(df)
    df.loc[length] = individual_row_data
 df
df.to_csv(r'C:\Users\ricky\Downloads\New folder\companies.csv',index =False)    

