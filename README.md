# World-Cup-Challenge-2022-ACM

<b>World Cup Challenge - 2022 ACM</b>

<b>Resumen de los modelos usados:</b>

En este script usamos o en si creamos 2 modelos de redes neuronales, uno que predice que equipo ganará y a la vez este modelo alimentará al modelo 2 el cual predice la cantidad de goles de un equipo a otro.


<b>Los datos que alimentan al modelo 1 son:</b>

* date: El año en que se realizo o jugo ese partido entre el equipo 1 y 2.

* Neutral: Si el partido se realiza en un lugar neutral o la casa de un equipo(1: neutral, 0: en la casa del primer equipo).

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
Qatar (1-1) Ecuador
Qatar (0-2) Senegal
Qatar (0-5) Netherlands
Ecuador (1-1) Senegal
Ecuador (1-2) Netherlands
Senegal (0-0) Netherlands

Ecuador_Qatar_+0
Senegal_Qatar_+2
Netherlands_Qatar_+5
Senegal_Ecuador_+0
Netherlands_Ecuador_+1
Netherlands_Senegal_+0

Netherlands {'win': 2.0, 'GF': 7.0, 'DG': 6.0}
Senegal {'win': 1.0, 'GF': 3.0, 'DG': 2.0}
Ecuador {'win': 0.0, 'GF': 3.0, 'DG': -1.0}
Qatar {'win': 0.0, 'GF': 1.0, 'DG': -7.0}

 ['Netherlands', 'Senegal'] 

 --------------------------------------------------
======================> Group B
England (1-0) Iran
England (1-0) United States
England (3-0) Wales
Iran (1-1) United States
Iran (0-1) Wales
United States (1-0) Wales

England_Iran_+1
England_United States_+1
England_Wales_+3
United States_Iran_+0
Wales_Iran_+1
United States_Wales_+1

England {'win': 3.0, 'GF': 5.0, 'DG': 5.0}
United States {'win': 1.0, 'GF': 2.0, 'DG': 0.0}
Wales {'win': 1.0, 'GF': 1.0, 'DG': -3.0}
Iran {'win': 0.0, 'GF': 1.0, 'DG': -2.0}

 ['England', 'United States'] 

 --------------------------------------------------
======================> Group C
Argentina (3-0) Saudi Arabia
Argentina (4-0) Mexico
Argentina (4-0) Poland
Saudi Arabia (1-2) Mexico
Saudi Arabia (1-4) Poland
Mexico (0-0) Poland

Argentina_Saudi Arabia_+3
Argentina_Mexico_+4
Argentina_Poland_+4
Mexico_Saudi Arabia_+1
Poland_Saudi Arabia_+3
Poland_Mexico_+0

Argentina {'win': 3.0, 'GF': 11.0, 'DG': 11.0}
Poland {'win': 1.0, 'GF': 4.0, 'DG': -1.0}
Mexico {'win': 1.0, 'GF': 2.0, 'DG': -3.0}
Saudi Arabia {'win': 0.0, 'GF': 2.0, 'DG': -7.0}

 ['Argentina', 'Poland'] 

 --------------------------------------------------
======================> Group D
France (2-1) Australia
France (0-0) Denmark
France (2-1) Tunisia
Australia (0-4) Denmark
Australia (0-1) Tunisia
Denmark (2-0) Tunisia

France_Australia_+1
Denmark_France_+0
France_Tunisia_+1
Denmark_Australia_+4
Tunisia_Australia_+1
Denmark_Tunisia_+2

Denmark {'win': 2.0, 'GF': 6.0, 'DG': 6.0}
France {'win': 2.0, 'GF': 4.0, 'DG': 2.0}
Tunisia {'win': 1.0, 'GF': 2.0, 'DG': -2.0}
Australia {'win': 0.0, 'GF': 1.0, 'DG': -6.0}

 ['Denmark', 'France'] 

 --------------------------------------------------
======================> Group E
Spain (2-0) Costa Rica
Spain (1-1) Germany
Spain (4-1) Japan
Costa Rica (2-3) Germany
Costa Rica (1-3) Japan
Germany (2-2) Japan

Spain_Costa Rica_+2
Germany_Spain_+0
Spain_Japan_+3
Germany_Costa Rica_+1
Japan_Costa Rica_+2
Japan_Germany_+0

Spain {'win': 2.0, 'GF': 7.0, 'DG': 5.0}
Germany {'win': 1.0, 'GF': 6.0, 'DG': 1.0}
Japan {'win': 1.0, 'GF': 6.0, 'DG': -1.0}
Costa Rica {'win': 0.0, 'GF': 3.0, 'DG': -5.0}

 ['Spain', 'Germany'] 

 --------------------------------------------------
======================> Group F
Belgium (2-0) Canada
Belgium (2-0) Morocco
Belgium (3-1) Croatia
Canada (1-0) Morocco
Canada (0-1) Croatia
Morocco (0-2) Croatia

Belgium_Canada_+2
Belgium_Morocco_+2
Belgium_Croatia_+2
Canada_Morocco_+1
Croatia_Canada_+1
Croatia_Morocco_+2

Belgium {'win': 3.0, 'GF': 7.0, 'DG': 6.0}
Croatia {'win': 2.0, 'GF': 4.0, 'DG': 1.0}
Canada {'win': 1.0, 'GF': 1.0, 'DG': -2.0}
Morocco {'win': 0.0, 'GF': 0.0, 'DG': -5.0}

 ['Belgium', 'Croatia'] 

 --------------------------------------------------
======================> Group G
Brazil (2-0) Serbia
Brazil (1-1) Switzerland
Brazil (1-0) Cameroon
Serbia (1-1) Switzerland
Serbia (1-0) Cameroon
Switzerland (2-0) Cameroon

Brazil_Serbia_+2
Switzerland_Brazil_+0
Brazil_Cameroon_+1
Switzerland_Serbia_+0
Serbia_Cameroon_+1
Switzerland_Cameroon_+2

Brazil {'win': 2.0, 'GF': 4.0, 'DG': 3.0}
Switzerland {'win': 1.0, 'GF': 4.0, 'DG': 2.0}
Serbia {'win': 1.0, 'GF': 2.0, 'DG': -1.0}
Cameroon {'win': 0.0, 'GF': 0.0, 'DG': -4.0}

 ['Brazil', 'Switzerland'] 

 --------------------------------------------------
======================> Group H
Portugal (2-1) Ghana
Portugal (1-0) Uruguay
Portugal (2-0) South Korea
Ghana (0-1) Uruguay
Ghana (2-0) South Korea
Uruguay (0-0) South Korea

Portugal_Ghana_+1
Portugal_Uruguay_+1
Portugal_South Korea_+2
Uruguay_Ghana_+1
Ghana_South Korea_+2
South Korea_Uruguay_+0

Portugal {'win': 3.0, 'GF': 5.0, 'DG': 4.0}
Ghana {'win': 1.0, 'GF': 3.0, 'DG': 0.0}
Uruguay {'win': 1.0, 'GF': 1.0, 'DG': 0.0}
South Korea {'win': 0.0, 'GF': 0.0, 'DG': -4.0}

 ['Portugal', 'Ghana'] 

 --------------------------------------------------
```


<h2>Octavos</h2>

```python
Netherlands (2-1) United States | Netherlands_United States_+1
Argentina (3-4) France | France_Argentina_+1
Spain (5-3) Croatia | Spain_Croatia_+2
Brazil (3-0) Ghana | Brazil_Ghana_+3
Senegal (0-1) England | England_Senegal_+1
Poland (3-1) Denmark | Poland_Denmark_+2
Germany (4-0) Belgium | Germany_Belgium_+4
Switzerland (1-0) Portugal | Switzerland_Portugal_+1
```

<h2>Cuartos</h2>

```python
Netherlands (0-2) France | France_Netherlands_+2
Spain (1-0) Brazil | Spain_Brazil_+1
England (3-1) Poland | England_Poland_+2
Germany (3-0) Switzerland | Germany_Switzerland_+3
```

<h2>Semifinales Y Finales</h2>

```python
France (1-0) Spain | France_Spain_+1
England (0-4) Germany | Germany_England_+4

Spain (4-0) England | Spain_England_+4

Fourth in the world cup: England
Third in the world cup: Spain

The Final is between: ['France', 'Germany']

France (0-2) Germany | Germany_France_+2

Second in the world cup: France

World Cup Winner is:  Germany
```

