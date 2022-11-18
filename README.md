# World-Cup-Challenge-2022-ACM

<b>World Cup Challenge - 2022 ACM</b>

<b>Resumen de los modelos usados:</b>

En este script usamos o en si creamos 2 modelos de redes neuronales, uno que predice que equipo ganará y a la vez este modelo alimentará al modelo 2 el cual predice la cantidad de goles de un equipo a otro.


<b>Los datos que alimentan al modelo 1 son:</b>

* Neutral: si el partido se realiza en un lugar neutral o la casa de un equipo(1: neutral, 0: en la casa del primer equipo).

* played 1: El número de partidos jugados por el primer equipo.

* played 2: El número de partidos jugados por el segundo equipo.

* win 1: El número de partidos ganados por el primer equipo.

* win 2: El número de partidos ganados por el segundo equipo.

* lose 1: El número de partidos perdidos por el primer equipo.

* lose 2: El número de partidos perdidos por el segundo equipo.

* win_1_vs_2: El número de partidos ganados por el primer equipo contra el segundo equipo.

* lose_1_vs_2: El número de partidos perdidos por el primer equipo contra el segundo equipo.

* total_1_vs_2: El número de partidos jugados por el primer equipo contra el segundo equipo.

* result: El resultado del partido, 1, entonces, gano el primer equipo, 2, entonces, gano el segundo equipo.

* Onehotenconder de todos los paises tanto para el primer equipo como el segundo, en total 632 columnas.


<br>
<b>Data usada para el modelo 2:</b>

* Neutral: si el partido se realiza en un lugar neutral o la casa de un equipo(1: neutral, 0: en la casa del primer equipo).

* played 1: El número de partidos jugados por el primer equipo.

* played 2: El número de partidos jugados por el segundo equipo.

* win 1: El número de partidos ganados por el primer equipo.

* win 2: El número de partidos ganados por el segundo equipo.

* lose 1: El número de partidos perdidos por el primer equipo.

* lose 2: El número de partidos perdidos por el segundo equipo.

* tie 1: El número de partidos empatados por el primer equipo.

* tie 2: El número de partidos empatados por el segundo equipo.

* win_1_vs_2: El número de partidos ganados por el primer equipo contra el segundo equipo.

* lose_1_vs_2: El número de partidos perdidos por el primer equipo contra el segundo equipo.

* tie_1_vs_2: El número de partidos empatados por el primer equipo contra el segundo equipo o viceversa.

* total_1_vs_2: El número de partidos jugados por el primer equipo contra el segundo equipo.

* result en onehotenconder, donde 0(empate, [0,0,0]), 1(gano el equipo 1, [0,1,0]), 2(gano el equipo 2, [0,0,1]), esta respuesta para predecirla al final será data por el modelo 1.

* Onehotenconder de todos los paises tanto para el primer equipo como el segundo, en total 632 columnas.



<br>
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
======================> Group A
Qatar (4-1) Ecuador
Qatar (1-0) Senegal
Qatar (0-0) Netherlands
Ecuador (0-1) Senegal
Ecuador (2-2) Netherlands
Senegal (0-0) Netherlands

Qatar_Ecuador_+3
Qatar_Senegal_+1
Netherlands_Qatar_+0
Senegal_Ecuador_+1
Netherlands_Ecuador_+0
Netherlands_Senegal_+0

Qatar {'win': 2.0, 'GF': 5.0, 'DG': 4.0}
Ecuador {'win': 1.0, 'GF': 4.0, 'DG': -2.0}
Senegal {'win': 0.0, 'GF': 0.0, 'DG': -2.0}
Netherlands {'win': 0.0, 'GF': 2.0, 'DG': 0.0}

 ['Qatar', 'Ecuador'] 

 --------------------------------------------------
======================> Group B
England (0-0) Iran
England (2-0) United States
England (2-0) Wales
Iran (2-1) United States
Iran (1-1) Wales
United States (1-0) Wales

Iran_England_+0
England_United States_+2
England_Wales_+2
Iran_United States_+1
Wales_Iran_+0
United States_Wales_+1

England {'win': 2.0, 'GF': 4.0, 'DG': 4.0}
Iran {'win': 1.0, 'GF': 3.0, 'DG': 1.0}
United States {'win': 1.0, 'GF': 2.0, 'DG': -2.0}
Wales {'win': 0.0, 'GF': 1.0, 'DG': -3.0}

 ['England', 'Iran'] 

 --------------------------------------------------
======================> Group C
Argentina (2-0) Saudi Arabia
Argentina (2-0) Mexico
Argentina (2-0) Poland
Saudi Arabia (0-2) Mexico
Saudi Arabia (0-1) Poland
Mexico (1-0) Poland

Argentina_Saudi Arabia_+2
Argentina_Mexico_+2
Argentina_Poland_+2
Mexico_Saudi Arabia_+2
Poland_Saudi Arabia_+1
Mexico_Poland_+1

Argentina {'win': 3.0, 'GF': 6.0, 'DG': 6.0}
Saudi Arabia {'win': 2.0, 'GF': 3.0, 'DG': 1.0}
Mexico {'win': 1.0, 'GF': 1.0, 'DG': -3.0}
Poland {'win': 0.0, 'GF': 0.0, 'DG': -4.0}

 ['Argentina', 'Saudi Arabia'] 

 --------------------------------------------------
======================> Group D
France (2-0) Australia
France (0-0) Denmark
France (4-2) Tunisia
Australia (1-3) Denmark
Australia (0-2) Tunisia
Denmark (2-1) Tunisia

France_Australia_+2
Denmark_France_+0
France_Tunisia_+2
Denmark_Australia_+2
Tunisia_Australia_+2
Denmark_Tunisia_+1

France {'win': 2.0, 'GF': 6.0, 'DG': 4.0}
Australia {'win': 2.0, 'GF': 5.0, 'DG': 2.0}
Denmark {'win': 1.0, 'GF': 3.0, 'DG': -1.0}
Tunisia {'win': 0.0, 'GF': 3.0, 'DG': -5.0}

 ['France', 'Australia'] 

 --------------------------------------------------
======================> Group E
Spain (4-2) Costa Rica
Spain (1-1) Germany
Spain (2-1) Japan
Costa Rica (0-5) Germany
Costa Rica (1-3) Japan
Germany (4-0) Japan

Spain_Costa Rica_+2
Germany_Spain_+0
Spain_Japan_+1
Germany_Costa Rica_+5
Japan_Costa Rica_+2
Germany_Japan_+4

Spain {'win': 2.0, 'GF': 7.0, 'DG': 3.0}
Costa Rica {'win': 2.0, 'GF': 10.0, 'DG': 5.0}
Germany {'win': 1.0, 'GF': 5.0, 'DG': -1.0}
Japan {'win': 0.0, 'GF': 2.0, 'DG': -7.0}

 ['Costa Rica', 'Spain'] 

 --------------------------------------------------
======================> Group F
Belgium (2-0) Canada
Belgium (1-0) Morocco
Belgium (1-0) Croatia
Canada (0-2) Morocco
Canada (0-1) Croatia
Morocco (2-1) Croatia

Belgium_Canada_+2
Belgium_Morocco_+1
Belgium_Croatia_+1
Morocco_Canada_+2
Croatia_Canada_+1
Morocco_Croatia_+1

Belgium {'win': 3.0, 'GF': 4.0, 'DG': 4.0}
Canada {'win': 2.0, 'GF': 3.0, 'DG': 1.0}
Morocco {'win': 1.0, 'GF': 2.0, 'DG': -2.0}
Croatia {'win': 0.0, 'GF': 1.0, 'DG': -3.0}

 ['Belgium', 'Canada'] 

 --------------------------------------------------
======================> Group G
Brazil (1-0) Serbia
Brazil (1-1) Switzerland
Brazil (3-0) Cameroon
Serbia (1-1) Switzerland
Serbia (2-0) Cameroon
Switzerland (3-0) Cameroon

Brazil_Serbia_+1
Switzerland_Brazil_+0
Brazil_Cameroon_+3
Switzerland_Serbia_+0
Serbia_Cameroon_+2
Switzerland_Cameroon_+3

Brazil {'win': 2.0, 'GF': 5.0, 'DG': 4.0}
Serbia {'win': 1.0, 'GF': 3.0, 'DG': 1.0}
Switzerland {'win': 1.0, 'GF': 5.0, 'DG': 3.0}
Cameroon {'win': 0.0, 'GF': 0.0, 'DG': -8.0}

 ['Brazil', 'Switzerland'] 

 --------------------------------------------------
======================> Group H
Portugal (2-1) Ghana
Portugal (1-1) Uruguay
Portugal (0-2) South Korea
Ghana (0-2) Uruguay
Ghana (1-0) South Korea
Uruguay (2-0) South Korea

Portugal_Ghana_+1
Uruguay_Portugal_+0
South Korea_Portugal_+2
Uruguay_Ghana_+2
Ghana_South Korea_+1
Uruguay_South Korea_+2

Portugal {'win': 2.0, 'GF': 5.0, 'DG': 3.0}
Ghana {'win': 2.0, 'GF': 4.0, 'DG': 2.0}
Uruguay {'win': 1.0, 'GF': 3.0, 'DG': 0.0}
South Korea {'win': 0.0, 'GF': 0.0, 'DG': -5.0}

 ['Portugal', 'Ghana'] 

 --------------------------------------------------
```


<h2>Octavos</h2>

```python
Qatar (0-2) Iran | Iran_Qatar_+2
Ecuador (0-1) England | England_Ecuador_+1
Argentina (2-1) Australia | Argentina_Australia_+1
Saudi Arabia (0-4) France | France_Saudi Arabia_+4
Costa Rica (1-0) Canada | Costa Rica_Canada_+1
Spain (3-1) Belgium | Spain_Belgium_+2
Brazil (1-0) Ghana | Brazil_Ghana_+1
Switzerland (2-1) Portugal | Switzerland_Portugal_+1
```

<h2>Cuartos</h2>

```python
Iran (0-2) England | England_Iran_+2
Argentina (1-0) France | Argentina_France_+1
Costa Rica (2-4) Spain | Spain_Costa Rica_+2
Brazil (3-0) Switzerland | Brazil_Switzerland_+3
```

<h2>Semifinales Y Finales</h2>

```python
England (1-2) Argentina | Argentina_England_+1
Spain (0-2) Brazil | Brazil_Spain_+2

England (2-1) Spain | England_Spain_+1

Fourth in the world cup: Spain
Third in the world cup: England

The Final is between: ['Argentina', 'Brazil']

Argentina (2-1) Brazil | Argentina_Brazil_+1

Second in the world cup: Brazil

World Cup Winner is:  Argentina
```

