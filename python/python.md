https://www.python.org/

2 個都勾

pip install requests

pip install BeautifulSoup4
-> html 解析器


pip install notebook


jupyter notebook

右邊 New

Python 3 (ipykernel)

import requests
from bs4 import BeautifulSoup

response=requests.get("")

print(response)

soup=BeautifulSoup(response.text,"html.parser")

print(soup)


print(soup.find("h1"))
-><h1>歡迎</h1>


print(soup.find("h1").text)
->歡迎


print(soup.select("title"))
->[<title>test </title>]


print(soup.select("title")[0].text)
->test 


正則表達式

* __ 前一字元或括號內字元出現0次或多次 __ a*b* __ aaaab、aabb、bbb

+ __ 前一字元或括號內字元出現1次或多次 __ a+b+ __ aaabb、abbbb、abbbbb

{m,n} __ 前一字元或括號內字元出現m次到n次(包含m,n) __ a{1,2}b{3,4} __ abbb、aabbbb、aabbb

[] __ 符合括號內的任一字元 __ [A-Z]+ __ APPLE、QWER

\ __ 跳脫字元 __ \. \+ \* __ .|\


import re
pattern = "a*b+c"
string = " find aabc ac skip abb,dd "
re.findall(pattern,string)

->['aabc']


import re
pattern = "[0-9]+"
string = "12個22個35 個"
re.findall(pattern,string)

->['12', '22', '35']


list_temp=re.findall(pattern,string)
list_temp[1]

-> '12'



import re
pattern = "123"
string = "abc123, ser123"
re.findall(pattern,string)

->['123', '123']



import re
pattern = "[cmf]an"

cmf三種都可以，後面加an

string = "find canmanfanasd"
re.findall(pattern,string)

->['can','man','fan']



import re
pattern = "jim{2,5}y"
string = "findjimmyjimmmmmy"
re.findall(pattern,string)

->['jimmy','jimmmmmy']




import re
pattern = "lovecat|lovecat"

|代表左右邊只要任一符合條件即可

string = "find lovecat,sdfjfjlovedog"
re.findall(pattern,string)

->['lovecat','lovecat']



import re
pattern = "neo|ne{3}o"

|代表左右邊只要任一符合條件即可

string = "findneoneeoneeeoneeeeo"
re.findall(pattern,string)

->['neo','neeeo']



import requests
from bs4 import BeautifulSoup
import re
res=requests.get("")
soup=BeautifulSoup(res.text,"html.parser")
soup
soup.find_all(re.compile("t{d|r}"))
-> 找出 td tr 標籤

soup.find_all(href=re.compile("^http"))
-> 找出 href 並且有 http

soup.find_all("",text=re.compile("我"))
-> 找出有 我 的資訊的

list_temp=soup.find_all("",text=re.compile("我"))
list_temp[1]



pip install lxml

import requests
from bs4 import BeautifulSoup
import re

res=requests.get("")
res.encoding='utf-8'
soup=BeautifulSoup(res.text,"lxml")

soup

address1=soup.find_all("",text=re.compile('街'))
address2=soup.find_all("",text=re.compile('路'))

phone=soup.find_all("span")

phone=str(phone)

re.findall("0[1-9]+-[0-9]+",phone)

re.findall("0[1-9]+",phone)

re.findall("0[1-9]{9}",phone)


https://www.twse.com.tw/zh/page/trading/exchange/STOCK_DAY_AVG.html


