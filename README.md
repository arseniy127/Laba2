# Laba2
import requests
import json
import matplotlib
import matplotlib.pyplot
mas=[]
for page in range(0,10):
    r=requests.get('https://api.hh.ru/vacancies?page=%s&per_page=100' % page)
    items = r.json()['items']
    for i in items:
        professions = {i['name']:i['salary']}
        mas.append(professions);
mes=[]
mes = [i for i in mas if [k for k in i if i[k]!= None]]
mid=[]
for i in mes:
    for k in i:
        if i[k]['from'] != None and i[k]['to'] != None:
            mi={k : (int(i[k]['from'])+int(i[k]['to']))/2}
        elif i[k]['from'] == None and i[k]['to'] != None:
            mi={k:i[k]['to']}
        elif i[k]['from'] != None and i[k]['to'] == None:
            mi={k:i[k]['from']}
        mid.append(mi)
for i in range(len(mid)-1):
    for j in range(len(mid)-i):
        for k1 in mid[i].keys():
            for k2 in mid[j].keys():
                if k1<k2:
                    str=mid[j]
                    mid[j]=mid[i]
                    mid[i]=str    
med=[]
sred=[]
for myi in range(len(mid)-1):
     for k1, v1 in mid[len(mid)-1-myi].items():
            for k2, v2 in mid[len(mid)-2-myi].items():
                if k1==k2: 
                    sred.append(v1)
                else:
                    sred.append(v1)
                    if (len(sred) % 2) != 0:
                        el = {k1:sred[(len(sred)//2)]}
                    else:
                        el = {k1:(sred[len(sred)//2]+sred[(len(sred)//2)-1])/2}
                    med.append(el)
                    l=len(sred)
                    for k in range(l):
                        sred.pop(l-1-k)
masss=[]
for i in med:
    for j in i.values():
        masss.append(j)
matplotlib.pyplot.hist(masss)
