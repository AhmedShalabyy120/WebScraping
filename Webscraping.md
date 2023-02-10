
Creating a webscraping tool , to get the data from a books website 
using many libraries like BeautifulSoup
pandas
time

====
import csv 
from bs4 import BeautifulSoup
import requests
import pandas as pd
import time
import random
=====
try:

    page=1
    counter=1
    with open('D:\web scrapping\jobs2.diwan','a',newline='',encoding='utf-8') as f:
            writer=csv.writer(f)
            writer.writerow(['Title','Author','Price'])
            while True:
                url=requests.get(f'https://diwanegypt.com/product-category/books/arabic-books/page/{page}/')
                soup=BeautifulSoup(url.content,'lxml')
                all_books=soup.find('div',class_='inner')
                card_book=all_books.find_all('li',class_='status-publish')
                page_limit=int(len(all_books.find_all('li',class_='status-publish')))


                for i in range(len(card_book)):
                    title=card_book[i].find('h2',class_='woocommerce-loop-product__title').text.strip()
                    author=card_book[i].find('span',class_='author').text.strip()
                    price=card_book[i].find('span',class_='amount').text
                    writer.writerow([title,author,price])
                counter +=1
                print(counter)        
                page+=1
                if page_limit ==0:
                    break
                time.sleep(random.uniform(2, 5))
                
except Exception as e:
    print(f'Error: {e}')
                    
           
            
