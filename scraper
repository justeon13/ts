from bs4 import BeautifulSoup
import requests
import textwrap
import pandas

l=[]
base_url="https://www.yachtworld.com/core/listing/cache/searchResults.jsp?sm=3&searchtype=homepage&Ntk=boatsEN&ftid=0&Ns=PBoat_sortByPriceAsc%7C0&enid=0&toYear=2018&hmid=0&type=%28Sail%29&boatsAddedSelected=-1&slim=quick&currencyid=100&fromPrice=0&luom=126&rid=107&rid=108&toLength=45&fromLength=32&cit=true&fromYear=1990&ps=50&No="
for page in range(0,200,50):
    print(base_url+str(page))
    r=requests.get(base_url+str(page))
    c=r.content
    soup=BeautifulSoup(c,"html.parser")
    all=soup.find_all("div",{"class":"information"})
    for item in all:
        d={}
        d["Sailboat"]=textwrap.shorten(item.find("div",{"class":"make-model"}).text,width=50)
        if item.find("div",{"class":"price"}).text.replace("\n","").replace("*","").replace(" ","") == 'Call$(".currNote").hide()':
            d["Price"]=("Call for current price")
        else:
            d["Price"]=item.find("div",{"class":"price"}).text.replace("\n","").replace("*","").replace(" ","")
        d["Location"]=textwrap.shorten(item.find("div",{"class":"location"}).text,width=50)
        d["Broker"]=textwrap.shorten(item.find("div",{"class":"broker"}).text,width=50)
        l.append(d)

df=pandas.DataFrame(l)
df.to_csv("West Coast Sailboats for Sale From Yacht Finder.csv")
