# Premier League 2021-2022 (EDA)

A Premier League é um torneio de futebol originário da Inglaterra, e tal torneio é considerado como um dos campeonatos mais reconhecíveis e aclamados pela crítica, justamente por ser um dos campeonatos de maior qualidade futebolística e competitiva. 

Neste projeto analítico, apresento em minúcias uma análise exploratória concernente à Premier League da edição mais recente de 2021-2022, em tal exame, responderei diversas questões que exponham vários insights informacionais relevantes e nevrálgicas em relação à última edição de tal campeonato.

![](./img/Premier_League_Logo.svg.png)

## Importação de bibliotecas:

Às bibliotecas importadas para essa análise foram Pandas, Numpy, Matplotlib e Seaborn, Pandas e Numpy são bibliotecas que fornecem funções tabulares que facilitam na manipulação dos dados, já Matplotlib e Seaborn são bibliotecas alternantes que fornecem plotagens gráficas que facilitam na visualização dos dados analisados.

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

```

## Fonte de dados:

O dataset [English Premier League 2021-22 Match Data](https://www.kaggle.com/datasets/evangower/premier-league-match-data) está disponível no Kaggle para uso gratuito.

## **(1)** Tratamento dos dados:

O conjunto de dados que foi utilizado na análise contêm 380 linhas e 22 colunas, às 380 linhas representam cada partida registrada e às 22 colunas representam variáveis relativas à dados estatísticos dos times mandantes ou visitantes de cada partida durante o campeonato. 

* Renomeação de colunas:

Primeiramente, antes de iniciar a análise, tive que renomear às colunas para que pudesse ter colunas com nomes intuitivos e objetivos sobre o quê tais variáveis e características representavam na tabela.

Original às colunas estavam com tais nomes:


```
['Date', 'HomeTeam', 'AwayTeam', 'FTHG', 'FTAG', 'FTR', 'HTHG', 'HTAG',
       'HTR', 'Referee', 'HS', 'AS', 'HST', 'AST', 'HF', 'AF', 'HC', 'AC',
       'HY', 'AY', 'HR', 'AR']

```
Notavelmente, é observável que somente quatro colunas possuem um nome entendível sobre às características aos quais se referem, logo tive que modificar o nome das demais colunas de acordo com o que tais colunas representam:

```
['date', 'hometeam', 'awayteam', 'home_goals', 'away_goals', 'result',
       'referee', 'home_shots', 'away_shots', 'home_fouls', 'away_fouls',
       'home_corners', 'away_corners', 'home_yellow_cards',
       'away_yellow_cards', 'home_red_cards', 'away_red_cards']

```
Os nomes das colunas foram modificáveis condizentemente com às informações instrutivas que foram dadas no Kaggle em relação ao que cada coluna do dataset significava e representava.

