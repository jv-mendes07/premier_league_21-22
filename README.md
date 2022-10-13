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

Após a fase de limpeza e tratamento dos dados, criei duas novas colunas na tabela, a primeira coluna representava a quantidade de gols totais registrados por partida e a segunda coluna representava a soma acumulativa de gols durante o campeonato até a última partida.

```
df = df.assign(total_goals = df['home_goals'] + df['away_goals'],
          acumulative_goals = (df['home_goals'] + df['away_goals']).cumsum())
```

Concluída a fase de pré-análise em que os dados foram limpados e tratados, iniciei a análise exploratória com uma dúvida pertinente em relação ao campeonato inglês de tal edição:

#### **(1)** Durante o campeonato todo, houve mais registros de vitórias de times mandantes ou visitantes? E qual foi a quantidade de empates contabilizados?

Basicamente, no meio futebolístico há uma tendência popular na crença dos torcedores de que os times mandantes apresentam mais probabilidade de vencerem os jogos do que os times visitantes, em defluência de que os **(a)** times mandantes estão mais acostumados à jogar em seus próprios estádios do que os times visitantes, e também **(b)** os times mandantes tendem à receber mais apoio e incentivo dos torcedores, e tal incentivo psicologicamente ajuda os jogadores do time da casa à terem mais confiança para o jogo, em contrapartida à desaprovação e a vaia constante dos torcedores da casa contra o time visitante geraria um efeito psiquíco nos jogadores visitantes de insegurança e nervosismo para o jogo.

Para que pudesse ter evidências que corroborassem tal conclusão acima, plotei um gráfico de barras para que uma parte da **(1)** pergunta fosse respondida diretamente:

![](./img/grafico_1.png)

O gráfico de barras horizontais acima informa que os times mandantes coletaram mais vitórias em comparação aos times visitantes durante todo o campeonato inglês, precisamente houve o registro de 163 vitórias para os times mandantes dos jogos e 129 vitórias para os times visitantes, ou seja, comparativamente há uma diferença de 39 vitórias de times mandantes em relação aos times visitantes.

Já os demais 88 jogos foram de jogos que resultaram em empate, assim após obter a quantidade de vitórias para times mandantes ou visitantes, junto com a quantidade de empates, trouxe em sequência um gráfico de pizza para responder completamente a **(1)** questão:

![](./img/grafico_2.png)

Como é observável acima, 43 % dos jogos resultaram em vitórias para times mandantes, 34 % para times visitantes e uma parcela minoritária de 22 % dos jogos resultaram em empates.

Após isto, será que poderia afirmar que times mandantes tendem à vencer mais jogos ou marcar mais gols do que times visitantes? Não exatamente, irei aprofundar-me em tal problema em questões ulteriores.

Respondida à questão **(1)**, irei responder às perguntas mais óbvias que tenderiam à surgir na mente de qualquer um que fizesse essa análise:

#### **(2)** Quais foram os times que mais contabilizaram vitórias durante o campeonato?

Para responder tal questão, tive que criar uma coluna que informasse qual time foi o vencedor de cada partida, e consequentemente realizei um agrupamento dos times vencedores pela quantidade de vitórias contabilizadas para saber em ordem decrescente quais foram os times que mais venceram e quais foram os times que menos venceram durante todo o campeonato.

A tabela abaixo traz informações sobre a quantidade de vitórias por time ordenada decrescentemente:

|     winner     | qtd |
|:--------------:|:---:|
|    Man City    |  29 |
|    Liverpool   |  28 |
|    Tottenham   |  22 |
|     Arsenal    |  22 |
|     Chelsea    |  21 |
|   Man United   |  16 |
|    West Ham    |  16 |
|     Wolves     |  15 |
|    Leicester   |  14 |
|   Aston Villa  |  13 |
|    Newcastle   |  13 |
|    Brentford   |  13 |
|    Brighton    |  12 |
| Crystal Palace |  11 |
|     Everton    |  11 |
|      Leeds     |  9  |
|   Southampton  |  9  |
|     Burnley    |  7  |
|     Watford    |  6  |
|     Norwich    |  5  |

Com a tabela acima, plotei um gráfico de barras para expor a quantidade de vitórias por time de modo mais visual e mais fácil de ser entendível por qualquer um que fosse obter tal informação:

![](./img/grafico_3.png)

Como é observável no gráfico acima, Manchester City que foi o time campeão, como expectante, também foi o time que mais obteve vitórias durante o campeonato, já os times que ficaram em posições abaixo do Manchester City na tabela da Premier League tiveram menos vitórias contábeis, Liverpool que foi o vice-campeão, também foi o segundo time com mais vitórias no campeonato.

Chelsea teve menos vitórias contabilizadas em comparação ao Arsenal e ao Tottenham, porém como o Chelsea teve mais empates e menos derrotas do que esses dois times, então o Chelsea teve um término de campeonato em terceiro lugar, na frente do Arsenal e do Tottenham.

Após a **(2)** questão ter sido respondida, poderei explorar mais questões óbvias que qualquer um faria ao analisar tal conjunto de dados:

#### **(3)** Quais foram os times que mais contabilizaram derrotas durante o campeonato?

Novamente, o processo manipulatório para responder tal pergunta foi semelhante ao da questão anterior, criei uma coluna dos times perdedores de cada partida e depois agrupei-os pela quantidade de derrotas que estes times contabilizaram.

Um gráfico de barras é reiteradamente adequado para saber a quantidade de derrotas por cada time:

![](./img/grafico_4.png)

É vísivel que os times que mais venceram no campeonato como o Manchester City, Liverpool e Chelsea, foram logicamente os times que menos perderam durante o torneio, já os times que mais contabilizaram derrotas como o Norwich e o Watford foram os times que também foram rebaixados para a segunda divisão da Premier League.

No entanto, curiosamente o Burnley foi o oitavo time com mais derrotas acumulados, e mesmo assim foi um dos três times rebaixados para a segunda divisão, ou seja, Burnley foi um dos times com menos derrotas contabilizadas, mas também foi um dos times com menos vitórias e com mais empates acumulados, isto significa que seus adversários que contabilizaram mais derrotas, empataram menos e venceram mais jogos do que o Burnley para coloca-lo na segunda divisão.

Tal informação acima demonstra que não basta vencer mais para vencer o campeonato ou que basta perder menos para evitar o rebaixamento, a combinação da quantidade de vitórias, derrotas e empates será matematicamente crucial para determinar qual time será o campeão ou quais times serão rebaixados.

Respondida às duas questões mais importantes em relação a quantidade de vitórias e derrotas contabilizadas por cada time, tratarei sobre os empates registrados no campeonatos:

#### **(4)** Quais foram os times com mais empates contabilizados durante o campeonato?

Para responder tal questão, contabilizei a quantidade de empates de times mandantes e de times visitantes em tabelas separadas, depois utilizei a função pd.merge() do Pandas para juntar às duas tabelas em uma só, após isto, criei uma coluna com a quantidade de empates dos times ao jogarem como mandantes ou visitantes, e por fim obtive a quantidade total de empates registradas por cada time no campeonato.

Mais uma vez, usei o gráfico de barras para resolver tal problema, justamente por tal gráfico ser o mais recomendável para responder esse tipo de pergunta:

![](./img/grafico_5.png)

Chelsea foi um dos cinco times que mais empataram no campeonato, e por essa quantidade de empates, mesmo que o time tivesse tido uma quantidade de vitórias minimamente inferior do que Arsenal e Tottenham, o Chelsea conseguiu terminar o torneio como um dos três melhores times da temporada.

Em contrapartida, como já foi dito, o Burnley foi um dos times que mais foi derrotado e que mais teve empates no torneio, porém por ter sido um dos times com menos vitórias, conseguiu ser rebaixado por outros times que mesmo que tivessem mais derrotas e menos empates, ultrapassaram-o por ter mais vitórias.

Concluída a séries de perguntas e resposta em relação a quantidade de vitórias, derrotas e empates dos times, irei retornar às questões relativas aos times mandantes e visitantes do campeonato:

#### **(5)** No campeonato como um todo, houve mais gols marcados por times mandantes ou por times visitantes?
