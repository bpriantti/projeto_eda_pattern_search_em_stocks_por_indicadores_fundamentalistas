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

> Observou-se que a base possui uma série de dados faltantes listados com o valor 0, então a partir desse ponto substitui-se os valores e realizou-se uma análise visual da integridade dos dados por meio de um gráfico de heatmap, como demostrao na imagem abaixo:


Index(['Papel', 'Cotação', 'P/L', 'P/VP', 'PSR', 'Div.Yield', 'P/Ativo',
       'P/Cap.Giro', 'P/EBIT', 'P/Ativ Circ.Liq', 'EV/EBIT', 'EV/EBITDA',
       'Mrg Ebit', 'Mrg. Líq.', 'Liq. Corr.', 'ROIC', 'ROE', 'Liq.2meses',
       'Patrim. Líq', 'Dív.Brut/ Patrim.', 'Cresc. Rec.5a'],
      dtype='object')
      
Features targets:
> implementar o que é cada indicador  


