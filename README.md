# hello_world

# -*- coding: utf-8 -*-
#----------------------
# auther:zhangyy
#----------------------

from urllib.request import urlopen
from urllib.error import HTTPError, URLError
from bs4 import BeautifulSoup


def get_title(url):
    try:
        html = urlopen(url)
    except (HTTPError, URLError) as e:
        return None
    try:
        bsObj = BeautifulSoup(html.read(), "html.parser")
        title = bsObj.body.h1
    except AttributeError as e:
        return None
    return title

title = get_title("http://www.pythonscraping.com/pages/warandpeace.html")
if title == None:
    print("Title could not be found")
else:
    print(title.get_text())

print("========================我是猥琐的分隔符==========================")

html = urlopen("http://www.pythonscraping.com/pages/warandpeace.html")
bsObj = BeautifulSoup(html, "html.parser")
name_list = bsObj.findAll("span", {"class": "green"})
for name in name_list:
    print(name.get_text())

print("========================我是猥琐的分隔符==========================")

html = urlopen("http://www.pythonscraping.com/pages/page3.html")
bsObj = BeautifulSoup(html, "html.parser")

for child in bsObj.find("table", {"id": "giftList"}).children:
    print(child)

print("========================我是猥琐的分隔符==========================")

for sibling in bsObj.find("table", {"id": "giftList"}).tr.next_siblings:
    print(sibling)
