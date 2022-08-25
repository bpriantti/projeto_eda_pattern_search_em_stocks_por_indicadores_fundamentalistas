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

<img src="https://github.com/bpriantti/projeto_eda_pattern_search_em_stocks_por_indicadores_fundamentalistas/blob/main/images/image_1.png?raw=true"  width="800" height = "250">

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

