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

Originalmente, às colunas estavam com tais nomes:


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

* Tipo dos dados:

A coluna 'date' relativa à data em que cada partida do campeonato inglês foi realizada, estava com o tipo de dados como 'object' ao invés de 'datetime64[ns]', tive que modificar o tipo de dados de tal variável de tipo textual para o tipo data, para que às propriedades de data de tal coluna fossem acessíveis durante a fase de análise e manipulação dos dados.

```
df.date = df.date.astype('datetime64[ns]')
```

## **(2)** Exploração dos dados:

Após a fase de limpeza e tratamento dos dados, criei duas novas colunas na tabela, a primeira coluna representava a quantidade de gols totais registrados por partida e a segunda coluna representava a soma acumulativa de gols durante o campeonato até determinada partida.

```
df = df.assign(total_goals = df['home_goals'] + df['away_goals'],
          acumulative_goals = (df['home_goals'] + df['away_goals']).cumsum())
```

Concluída a fase de pré-análise em que os dados foram limpados e tratados, iniciei a análise exploratória com uma dúvida pertinente em relação ao campeonato inglês de tal edição:

#### **(1)** Durante o campeonato todo, houve mais registros de vitórias de times mandantes ou visitantes? E qual foi a quantidade de empates contabilizados?

Basicamente, no meio futebolístico há uma tendência popular na crença dos torcedores de que os times mandantes apresentam mais probabilidade de vencerem os jogos do que os times visitantes, em defluência de que os **(a)** times mandantes estão mais acostumados à jogar em seus próprios estádios do que os times visitantes, e também **(2)** os times mandantes tendem à receber mais apoio e incentivo dos torcedores, e tal incentivo psicologicamente ajuda os jogadores do time da casa à terem mais confiança para o jogo, em contrapartida à desaprovação e a vaia constante dos torcedores da casa contra o time visitante geraria um efeito psiquíco nos jogadores visitantes de insegurança e nervosismo para o jogo.

Para que pudesse ter evidências que corroborassem tal conclusão acima, plotei um gráfico de barra para que uma parte da **(1)** pergunta fosse respondida diretamente:

![](./img/grafico_1.png)

O gráfico de barras horizontais acima informa que os times mandantes coletaram mais vitórias em comparação aos times visitantes durante todo o campeonato inglês, precisamente houve o registro de 163 vitórias para os times mandantes dos jogos e 129 vitórias para os times visitantes, ou seja, comparativamente há uma diferença de 39 vitórias de times mandantes em relação aos times visitantes.

Já 88 jogos foram de jogos que resultaram em empate, assim após obter a quantidade de vitórias para times mandantes ou visitantes, junto com a quantidade de empates, trouxe em sequência um gráfico de pizza para responder completamente a **(1)** questão:

![](./img/grafico_2.png)

Como é observável acima, 43 % dos jogos resultaram em vitórias para times mandantes, 34 % para times visitantes e uma parcela minoritária de 22 % dos jogos resultaram em empates.

Após isto, será que poderia afirmar que times mandantes tendem à vencer mais jogos ou marcar mais gols do que times visitantes? Não exatamente, irei aprofundar-me em tal problema em questões ulteriores.

Respondida à questão **(1)**, irei responder às perguntas mais óbvias que tenderiam à surgir na mente de qualquer um que fizesse essa análise:

#### **(2)** Quais foram os times que mais contabilizaram vitórias durante o campeonato?

Para responder tal questão, tive que criar uma coluna que informasse qual time foi o vencedor de cada partida, e consequentemente realizei um agrupamento dos times vencedores pela quantidade de vitórias contabilizada para saber em ordem decrescente quais foram os times que mais venceram e quais foram os times que menos venceram durante todo o campeonato. 

