# Projeto EDA Pattern Search em Stocks por Indicadores Fundamentalistas.

__Bussines Problem:__

> Durante a rotina de investimentos e asset allocation torna-se importante ter-se o conhecimento de qual ativo escolher para a composição da carteira esta atividade também chamada de stock picking pode-se ser desenvolvida levando em conta uma série de fatores e cenários, um ponto importante deste trabalho é o valuation, que consiste no ato de precificar uma empresa e ter uma estimativa do seu valor de mercado, para isso analisa-se uma série de variáveis em referentes às empresas e dentro dessas variáveis temos os indicadores fundamentalistas que são uma série de indicadores financeiros e contábeis que expressam a saúde financeira de uma empresa, nesse contexto torna-se necessário uma análise desses indicadores e posterior resultado em performance da empresa na bolsa de valores. 

__Objetivo:__

> Realizar uma exploratory data analysis objetivando o pattern search dentro dos indicadores fundamentalistas das ações listadas na b3 para o ano 2020, realizando um agrupamento(clustering) e posteriormente avaliando a performance nos próximos semestres  para cada cluster, o resultado final busca ter uma noção de qual região de agrupamento trouxe uma melhor performance em relação a risco retorno por meio dos indicadores fundamentalistas.

__Autor:__  
   - Bruno Priantti.
    
__Contato:__  
  - bpriantti@gmail.com

__Encontre-me:__  
   -  https://www.linkedin.com/in/bpriantti/  
   -  https://github.com/bpriantti
   -  https://www.instagram.com/brunopriantti/
   
__Frameworks Utilizados:__

- Numpy: https://numpy.org/doc/  
- Pandas: https://pandas.pydata.org/
- Matplotlib: https://matplotlib.org/ 
- Seaborn: https://seaborn.pydata.org/  
- Plotly: https://plotly.com/  
- Scikit learn: https://scikit-learn.org/stable/index.html
- Statsmodels: https://www.statsmodels.org/stable/index.html

___

__Project Steps:__


__1 - import database:__

> A primeira etapa para esse projeto foi  a extração da base de dados dos indicadores fundamentalistas essa que só foi possível graças ao site ( fundamentus), foi possível extrair do site a base com os indicadores para um total de 900 ações listadas na bolsa de valores brasileira, o histórico da base é do período de 2020, realizou-se o load da base para posterior data wralling,

__2 - data wralling:__

> Observou-se que a base possui uma série de dados faltantes listados com o valor 0, então a partir desse ponto substitui-se os valores e realizou-se uma análise visual da integridade dos dados por meio de um gráfico de heatmap, como demonstrado na imagem abaixo no campo (base before wralling) para solução desse defeito de market data realizou-se a técnica de 'dropna()' utilizando o parâmetro thresh, setado em um valor de 17, ou seja só sobreviveram as colunas que possuírem no mínimo 17 valores sem ser o valor nan(nulo), a imagem abaixo mostra o resultado antes e depois para a base de dados.

   > <img src="https://github.com/bpriantti/projeto_eda_pattern_search_em_stocks_por_indicadores_fundamentalistas/blob/main/images/image_1.png?raw=true"  width="800" height = "250">

__3 - inspect colunas dataframe:__

> Em seguida verificou-se os indicadores fundamentalistas em que se tinha disponível, como observado abaixo possuímos os indicadores:

Index(['P/L', 'P/VP', 'PSR', 'Div.Yield', 'P/Ativo','P/Cap.Giro', 'P/EBIT', 'P/Ativ Circ.Liq', 'EV/EBIT', 'EV/EBITDA',
       'Mrg Ebit', 'Mrg. Líq.', 'Liq. Corr.', 'ROIC', 'ROE', 'Patrim. Líq', 'Dív.Brut/ Patrim.'], dtype='object')
       
- Descrição indicadores:  

  - Preço Lucro (P/L):  
    > O P/L é uma fórmula que estima o tempo considerando que a empresa mantenha os seus lucros, para que suas ações retornem ao investidor o valor investido.
  - Preço sobre Valor Patrimonial (P/VP):
    > O P/VP é um indicador fundamentalista que permite avaliar o preço de uma ação em relação ao valor do patrimônio líquido da empresa em um determinado período.
  - Price to Sales Ratio (Preço/Vendas) PSR:
    > O índice PSR é um indicador utilizado na análise fundamentalista para indicar o desempenho da receita líquida de uma companhia semelhante ao (P/L).
  - Div.Yield:
    > O dividend yield é um indicador que mede o rendimento de uma ação apenas com o pagamento de dividendos.
  - P/EBIT:
    > O P/EBIT indica a divisão entre o Preço da Ação e o EBIT de uma empresa por ação, uma sigla para Earning Before Interest and Taxes, ou Lucro Antes de Juros e           Impostos,em português.
  - P/Ativ Circ.Liq:
    > O P/Ativo Circulante Líquido representa a relação entre o preço da ação de uma companhia dividido pelos seus Ativos Circulantes Líquidos e os seus passivos.
  - EV/EBIT:
    > O EV/EBIT é um indicador fundamentalista que compara o Valor da Empresa (EV ou Enterprise Value) com o Lucro Antes de Impostos e Taxas, o EBIT.
  - EV/EBITDA:
    > O EV/EBITDA é um indicador que mostra a relação entre dois importantes indicadores o EV (Enterprise Value) e o EBITDA(earnings before interest, taxes,                 depreciation, and amortization) que mostra a receita após taxas e deveres.
  - Margem Ebit:
    > A margem EBIT é um indicador de desempenho operacional, usado para verificar o desempenho produtivo de uma empresa ao longo do tempo e para comparar a                 lucratividade operacional de companhias do mesmo segmento.
  - Margem Líquida
    > A margem líquida é o indicador financeiro que revela a porcentagem de lucro em relação às receitas que uma empresa apresentou no seu demonstrativo de resultados       trimestrais ou em seu consolidado anual.
  - Liquidez Corrente:
    > Liquidez corrente é um indicador financeiro que mostra a capacidade de uma empresa de quitar todas suas dívidas a curto prazo.
  - ROIC:
    > O ROIC (Return Over Invested Capital), ou Retorno sobre o Capital Investido, é uma métrica utilizada para informar, em termos percentuais, quanto dinheiro uma         empresa consegue gerar em razão do capital investido.
  - ROE:
    > O ROE (Return on Equity), ou Retorno sobre Patrimônio Líquido, é um indicador de rentabilidade que serve para determinar o quão eficiente é uma empresa na             geração de lucro a partir dos seus recursos
  - Patrimônio Líquido:
    > O Patrimônio Líquido é um indicador contábil que indica a relação entre os ativos e passivos financeiros de uma empresa.
  - Dívida Bruta/Patrimônio Líquido :
    > Relacao entre dívida e patrimônio líquido nos dá uma noção se a empresa tem fundos para quitar seus endividamentos ou não.

__4 - data visualization:__ base com indicadores fundamentalistas:

Visualizando distribuição dos indicadores para todas as empresas:

   > <img src="https://github.com/bpriantti/projeto_eda_pattern_search_em_stocks_por_indicadores_fundamentalistas/blob/main/images/image_2.png?raw=true"  width="800" height = "500">

__5 - load data base:__ performance próximos anos das empresas:

Os dados das empresas foram baixados via api-request do provedor yfinance, no processo de coleta de dados verificou-se que alguns tickers nao estavam disponiveis na plataforma estes sao:

23 Failed downloads:
- LAME4.SA: No data found, symbol may be delisted
- GNDI3.SA: No data found, symbol may be delisted
- GPCP3.SA: No data found, symbol may be delisted
- BRDT3.SA: No data found, symbol may be delisted
- FIBR3.SA: No data found for this date range, symbol may be delisted
- CCPR3.SA: No data found, symbol may be delisted
- VIVT4.SA: No data found, symbol may be delisted
- CESP3.SA: No data found, symbol may be delisted
- PNVL4.SA: No data found, symbol may be delisted
- RANI4.SA: No data found, symbol may be delisted
- CESP5.SA: No data found, symbol may be delisted
- JPSA3.SA: No data found, symbol may be delisted
- LAME3.SA: No data found, symbol may be delisted
- DTEX3.SA: No data found, symbol may be delisted
- TIET11.SA: No data found, symbol may be delisted
- CESP6.SA: No data found, symbol may be delisted
- HGTX3.SA: No data found, symbol may be delisted
- ELEK4.SA: No data found, symbol may be delisted
- ELEK3.SA: No data found, symbol may be delisted
- IGTA3.SA: No data found, symbol may be delisted
- TIET3.SA: No data found, symbol may be delisted
- TIET4.SA: No data found, symbol may be delisted
- WSON33.SA: No data found, symbol may be delisted

__2 - data wralling:__ base com preco de fechamentos das empresas:

- removendo nan's:
> Inicialmente verificou-se a quantidade de dados faltantes na base de dados, utilizando o metodo de heatmap por nan's e foram removidas as colunas com o dados faltantes, como ilustrado abaixo:

   > <img src="https://github.com/bpriantti/projeto_eda_pattern_search_em_stocks_por_indicadores_fundamentalistas/blob/main/images/image_3.png?raw=true"  width="800" height = "250">

- removendo defeitos de market data:
> Em seguida verificou-se dados com inconformidade de de atualização diária pelo provedor de dados, podemos visualizar nas ações com muitos dias com o mesmo preço pela imagem abaixo:

   > <img src="https://github.com/bpriantti/projeto_eda_pattern_search_em_stocks_por_indicadores_fundamentalistas/blob/main/images/image_4.png?raw=true"  width="700" height = "400">

> Normalmente visualizamos spikes de preços excessivos no momento em que o provedor de dados atualiza bases que estavam desatualizadas a dias, vamos verificar isso com um boxplot do retorno de todas as ações da base:

   > <img src="https://github.com/bpriantti/projeto_eda_pattern_search_em_stocks_por_indicadores_fundamentalistas/blob/main/images/image_5.png?raw=true"  width="700" height = "400">
   
> Em seguida visualizou-se os tickers que possuíam spikes acima de 2 ou -2, e grande parte deles possuía defeitos de market data mencionados, optou-se por remover esses tickers com dados defeituosos, observando a base novamente verificamos que os dados não possuíam mais dados com defeitos de market data por spikes defeituosos.

   > <img src="https://github.com/bpriantti/projeto_eda_pattern_search_em_stocks_por_indicadores_fundamentalistas/blob/main/images/image_6.png?raw=true"  width="700" height = "400">

- removendo defeitos de atualizacoes e dias seguidos:

> Verificou-se na base defeitos de dias seguidos, sabemos que por características das ações em momentos de baixa volatilidade os preços tendem a oscilar menos no entanto o defeito de dias seguidos pode ser definido com um range alto de dias por exemplo 20 dias sem atualizações de preço, isso provavelmente pode ser um defeito de market data, portanto desenvolveu-se uma função para verificar essas ocorrências e mostra-se o resultado na figura abaixo:

   > <img src="https://github.com/bpriantti/projeto_eda_pattern_search_em_stocks_por_indicadores_fundamentalistas/blob/main/images/image_7.png?raw=true"  width="700" height = "400">
   
obs: optou-se por remover esses tickers defeituosos.

- visualizando a base apos o processo de wralling:

obs: base de fechamentos foi normalizada para a base 100.

   > <img src="https://github.com/bpriantti/projeto_eda_pattern_search_em_stocks_por_indicadores_fundamentalistas/blob/main/images/image_8.png?raw=true"  width="700" height = "400">

__6 - wralling bases:__ alinhamento de tickers base de indicadores fundamentalistas e base com série de fechamentos:

Durante o procedimento de wralling foram removidos ticker
