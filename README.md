# World-Cup-Challenge-2022-ACM

World Cup Challenge - 2022 ACM

<b>1. Abrir el archivo "worlds cup 2k22 - predictor.ipynb" y crear una copia o abrirlo con tu cuenta de gmail.</b>

<b>2. Activar el GPU o el entorno de ejeucución del colab para que los modelos se entrenen más rapido.</b>

<b>3. Subir los archivos excel y json los cuales son la base de datos y un json generado gracias a esa base de datos.</b>
  
El json es un diccionario donde contiene las victorias, derrotas, y empates de un pais contra otro pais. Fue guardado en un json, ya que en si generar eso en codigo fue muy costoso computacionalmente.
   
 
 ```python
 def get_partys_teams(t1,t2):
  first = results[results['home_team']==t1]
  second = first[first['away_team']==t2]
  third = results[results['home_team']==t2]
  fourth = third[third['away_team']==t1]

  a = second[second['home_score']>second['away_score']].shape[0]
  a += fourth[fourth['home_score']<fourth['away_score']].shape[0]

  b = second[second['home_score']<second['away_score']].shape[0]
  b += fourth[fourth['home_score']>fourth['away_score']].shape[0]

  c = second[second['home_score']==second['away_score']].shape[0]
  c += fourth[fourth['home_score']==fourth['away_score']].shape[0]
  return [a,b,c]

print(get_partys_teams("Spain", "Brazil"), get_partys_teams("Brazil", "Spain"))

import json
table_1_vs_2 = {c+"_"+c2:get_partys_teams(c,c2) for c in countrys for c2 in countrys if c!=c2}
with open("data_1vs2.json", "w") as write_file:
    json.dump(table_1_vs_2, write_file)

with open("data_1vs2.json", "r") as read_file:
    table_1_vs_2 = json.load(read_file)
 
 ''' 
 OUTPUT:
 ([2, 5, 2], [5, 2, 2])
 '''
 ```
 
  
<b>4. Correr todas las celdas y esperar los resultados</b>

<h2>Grupos</h2>


```python
Groups = {"Group A": ["Qatar",  "Ecuador", "Senegal" ,"Netherlands"],
          "Group B": ["England",  "Iran", "United States",  "Wales"],
          "Group C": ["Argentina",  "Saudi Arabia",  "Mexico",  "Poland"],
          "Group D": ["France",  "Australia",  "Denmark",  "Tunisia"],
          "Group E": ["Spain",  "Costa Rica",  "Germany",  "Japan"],
          "Group F": ["Belgium",  "Canada",  "Morocco", "Croatia"],
          "Group G": ["Brazil", "Serbia",  "Switzerland",  "Cameroon"],
          "Group H": ["Portugal",  "Ghana", "Uruguay",  "South Korea"]}
```

```python
 =====================> Group A
Qatar (1-1) Ecuador
Qatar (2-1) Senegal
Qatar (0-2) Netherlands
Ecuador (0-2) Senegal
Ecuador (1-1) Netherlands
Senegal (2-0) Netherlands

Ecuador_Qatar_+0
Qatar_Senegal_+1
Netherlands_Qatar_+2
Senegal_Ecuador_+2
Netherlands_Ecuador_+0
Senegal_Netherlands_+2

Qatar {'win': 1.0, 'gols': 1.0}
Ecuador {'win': 0.0, 'gols': 0.0}
Senegal {'win': 2.0, 'gols': 4.0}
Netherlands {'win': 1.0, 'gols': 2.0}
['Senegal', 'Netherlands'] 
 --------------------------------------------------
 =====================> Group B
England (1-0) Iran
England (1-1) United States
England (2-0) Wales
Iran (1-1) United States
Iran (1-3) Wales
United States (2-0) Wales

England_Iran_+1
United States_England_+0
England_Wales_+2
United States_Iran_+0
Wales_Iran_+2
United States_Wales_+2

England {'win': 2.0, 'gols': 3.0}
Iran {'win': 0.0, 'gols': 0.0}
United States {'win': 1.0, 'gols': 2.0}
Wales {'win': 1.0, 'gols': 2.0}
['England', 'United States'] 
 --------------------------------------------------
 =====================> Group C
Argentina (2-0) Saudi Arabia
Argentina (2-0) Mexico
Argentina (1-1) Poland
Saudi Arabia (0-2) Mexico
Saudi Arabia (0-1) Poland
Mexico (0-1) Poland

Argentina_Saudi Arabia_+2
Argentina_Mexico_+2
Poland_Argentina_+0
Mexico_Saudi Arabia_+2
Poland_Saudi Arabia_+1
Poland_Mexico_+1

Argentina {'win': 2.0, 'gols': 4.0}
Saudi Arabia {'win': 0.0, 'gols': 0.0}
Mexico {'win': 1.0, 'gols': 2.0}
Poland {'win': 2.0, 'gols': 2.0}
['Argentina', 'Poland'] 
 --------------------------------------------------
 =====================> Group D
France (1-1) Australia
France (0-0) Denmark
France (2-1) Tunisia
Australia (1-1) Denmark
Australia (0-2) Tunisia
Denmark (2-1) Tunisia

Australia_France_+0
Denmark_France_+0
France_Tunisia_+1
Denmark_Australia_+0
Tunisia_Australia_+2
Denmark_Tunisia_+1

France {'win': 1.0, 'gols': 1.0}
Australia {'win': 0.0, 'gols': 0.0}
Denmark {'win': 1.0, 'gols': 1.0}
Tunisia {'win': 1.0, 'gols': 2.0}
['Tunisia', 'France'] 
 --------------------------------------------------
 =====================> Group E
Spain (2-0) Costa Rica
Spain (1-0) Germany
Spain (1-0) Japan
Costa Rica (2-1) Germany
Costa Rica (1-3) Japan
Germany (4-0) Japan

Spain_Costa Rica_+2
Spain_Germany_+1
Spain_Japan_+1
Costa Rica_Germany_+1
Japan_Costa Rica_+2
Germany_Japan_+4

Spain {'win': 3.0, 'gols': 4.0}
Costa Rica {'win': 1.0, 'gols': 1.0}
Germany {'win': 1.0, 'gols': 4.0}
Japan {'win': 1.0, 'gols': 2.0}
['Spain', 'Germany'] 
 --------------------------------------------------
 =====================> Group F
Belgium (2-0) Canada
Belgium (1-0) Morocco
Belgium (1-1) Croatia
Canada (0-1) Morocco
Canada (0-2) Croatia
Morocco (1-2) Croatia

Belgium_Canada_+2
Belgium_Morocco_+1
Croatia_Belgium_+0
Morocco_Canada_+1
Croatia_Canada_+2
Croatia_Morocco_+1

Belgium {'win': 2.0, 'gols': 3.0}
Canada {'win': 0.0, 'gols': 0.0}
Morocco {'win': 1.0, 'gols': 1.0}
Croatia {'win': 2.0, 'gols': 3.0}
['Belgium', 'Croatia'] 
 --------------------------------------------------
 =====================> Group G
Brazil (2-0) Serbia
Brazil (1-1) Switzerland
Brazil (2-0) Cameroon
Serbia (1-1) Switzerland
Serbia (0-3) Cameroon
Switzerland (0-0) Cameroon

Brazil_Serbia_+2
Switzerland_Brazil_+0
Brazil_Cameroon_+2
Switzerland_Serbia_+0
Cameroon_Serbia_+3
Cameroon_Switzerland_+0

Brazil {'win': 2.0, 'gols': 4.0}
Serbia {'win': 0.0, 'gols': 0.0}
Switzerland {'win': 0.0, 'gols': 0.0}
Cameroon {'win': 1.0, 'gols': 3.0}
['Brazil', 'Cameroon'] 
 --------------------------------------------------
 =====================> Group H
Portugal (2-1) Ghana
Portugal (1-1) Uruguay
Portugal (1-0) South Korea
Ghana (0-2) Uruguay
Ghana (0-1) South Korea
Uruguay (2-0) South Korea

Portugal_Ghana_+1
Uruguay_Portugal_+0
Portugal_South Korea_+1
Uruguay_Ghana_+2
South Korea_Ghana_+1
Uruguay_South Korea_+2

Portugal {'win': 2.0, 'gols': 2.0}
Ghana {'win': 0.0, 'gols': 0.0}
Uruguay {'win': 2.0, 'gols': 4.0}
South Korea {'win': 1.0, 'gols': 1.0}
['Uruguay', 'Portugal'] 
 --------------------------------------------------
```


<h2>Octavos</h2>

```python
Senegal (2-1) United States | Senegal_United States_+1
Netherlands (3-1) England | Netherlands_England_+2
Argentina (1-0) France | Argentina_France_+1
Poland (1-0) Tunisia | Poland_Tunisia_+1
Spain (2-0) Croatia | Spain_Croatia_+2
Germany (3-2) Belgium | Germany_Belgium_+1
Brazil (3-0) Portugal | Brazil_Portugal_+3
Cameroon (0-4) Uruguay | Uruguay_Cameroon_+4
```

<h2>Cuartos</h2>

```python
Senegal (1-4) Netherlands | Netherlands_Senegal_+3
Argentina (2-1) Poland | Argentina_Poland_+1
Spain (1-0) Germany | Spain_Germany_+1
Brazil (3-0) Uruguay | Brazil_Uruguay_+3
```

<h2>Semifinales Y Finales</h2>

```python
Netherlands (4-0) Argentina | Netherlands_Argentina_+4
Spain (0-2) Brazil | Brazil_Spain_+2

Argentina (2-1) Spain | Argentina_Spain_+1

Fourth in the world cup: Spain
Third in the world cup: Argentina

The Final is between: ['Netherlands', 'Brazil']

Netherlands (2-0) Brazil | Netherlands_Brazil_+2

Second in the world cup: Brazil

World Cup Winner is:  Netherlands
```

