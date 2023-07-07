# Análise paramétrica de uma LSTM aplicada a previsão de preço de cotações de ações

#### Aluno: [Jane Vieira Volotão](https://github.com/janevolotao/bimaster/).
#### Orientadora: [Manoela Kohler](https://github.com/manoelakohler).
---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso.

- [Link para o código - LSTM1](https://github.com/janevolotao/bimaster/LSTM1.ipynb).
- [Link para o código - LSTM2](https://github.com/janevolotao/bimaster/LSTM2.ipynb).
- [Link para o código - LSTM3](https://github.com/janevolotao/bimaster/LSTM3.ipynb). 
- [Link para o código - LSTM4](https://github.com/janevolotao/bimaster/LSTM4.ipynb). 
- [Link para o código - LSTM5](https://github.com/janevolotao/bimaster/LSTM5.ipynb). 
- [Link para o código - LSTM6](https://github.com/janevolotao/bimaster/LSTM6.ipynb).
---

### Resumo

Séries temporais tem sido estudadas pela Estatística através de métodos clássicos há várias décadas. Com o advento das técnicas de aprendizado profundo e inteligência artificial, novos métodos foram disponibilizados para previsão destas séries.
Este trabalho verificou a influência dos dados de entrada e da arquitetura da rede neural nos resultados obtidos numa previsão de série temporal. Dentre os diversos campos possíveis, foi escolhida uma série de cotações de ações da Petrobras na Bolsa de Valores.
Ao final uma configuração ótima de rede e parâmetros de entrada foi obtida baseado em valores mínimos de RMSE (Root Mean Square Error) e MAPE (Mean Absolute Percentage Error).

### 1. Introdução

A previsão de séries temporais pode ser considerada uma área de aplicação da mineração de dados preditiva. São coletadas observações de valores passados de uma ou mais variáveis e a partir da apresentação desses valores a um modelo,se tenta prever valores futuros para a série apresentada. É um assunto de ampla amplicação em diversos campos. Uma das áreas onde este assunto encontra uma aplicação direta é no mercado financeiro. Prever preço de ações na bolsa de valores tendo como base dados passados é ferramenta extremamente útil para investidores. Redes neurais recorrentes tem se mostrado uma técnica eficiente na previsão de séries temporais. 
Em especial as LSTM (Long Short Term Memory) por apresentar retroalimentação de camadas anteriores apresentam um desempenho satisfatório para aplicação em previsão de séries financeiras.

Neste trabalho foi realizada uma análise paramétrica para avaliar a influência dos dados de entrada utilizados em um previsão de série temporal por LSTM nos resultados obtidos.
Variou-se todos os parâmetros de entrada na construção da rede para buscar a configuração de desempenho ótimo. 
Ao final foram avaliadas métricas classicas de mensuração de erros em previsão de séries temporais por técnicas de aprendizado de máquina.

Para o estudo foram utilizadas cotações Ibovespa no fechamento de cada dia para ações Petrobras (PETR4).O período dos últimos 3 anos (25/05/2020 a 23/05/2023) foram utilizados nos estudos.

### 2. Modelagem

Uma célula LSTM tem três portões (gates), cada um dos quais é usado para modular sua entrada de alguma forma:um portão de entrada, um portão de esquecimento e um portão de saída. Tem uma "memória" e uma saída que são modificadas pelos portões. Ou seja, dentro de uma única célula LSTM:

(input & previous cell state) -> (input & forget gates) -> (update cell state)

(input & previous cell state & updated cell state) -> (output gate)

Foram variados parâmetros de entrada em intervalos de valores considerados factíveis em duas etapas consecutivas.Numa primeira etapa os valores de window, epochs e batch foram variados, mantendo a arquitetura da rede neural sem modificação.Nesta etapa foi utilizada a rede com a primeira camada com 100 neurônios, a segunda camada com 80 neurônios e a terceira camada com 50 neurônios.Na segunda etapa foram utilizados os parâmetros considerados ótimos na primeira etapa e a arquitetura da rede foi variada. Os números de neurônios das 3 camadas foram variados e encontrou-se a arquitetura ótima.

### 3. Resultados

As métricas de avaliação clássicas de avaliação de redes neurais foram utilizadas para classificar o desempenho das diversas configurações testadas.
São elas:.
- MSE:.
Fornece o erro na dimensão da variável e mede a magnitude média do erro.
- RMSE:.
Trata da raiz do MSE. Como o mesmo, fornece uma grandeza de erro na dimensão da variável e consegue representar a magnitude média do erro.	
- MAPE:.	
O MAPE tenta capturar a importância do erro relativo, fornecendo um valor percentual. Diferente do MSE e RMSE, esta métrica não guarda relação com o intervalo de variação dos dados de origem. Por ser um valor percentual torna mais prática sua avaliação como qualidade do modelo proposto.
- R2:.
R2 representa a porcentagem de variação na resposta que é explicada pelo modelo. Quanto maior o valor de R2 melhor está o ajuste de seu modelo aos dados de origem.	
- R2 adj:.
R2 ajustado foi desenvolvido buscando resolver um problema recorrente no uso do R2. Este problema surge quando adicionamos variáveis independentes ao problema. Independentemente do grau de causualidade na nova variável independente em relação ao meu modelo, R2 sempre aumenta quando acrescentamos novas variáveis. Com a equação de R2 ajustado, este problema se resolve. Como R2, representa a porcentagem de variação na resposta que é explicada pelo modelo. Quanto maior o valor de R2 ajustado melhor está o ajuste de seu modelo aos dados de origem.

A análise paramétrica das LSTM foi documentada em uma tabela no arquivo LSTM_PETR4.xlsx.

Na primeira etapa conclui-se que os parâmetros de entrada ótimos entre os avaliados foi:

- window: 15.
- batch: 64.
- epochs: 100.

Na segunda etapa concluiu-se que a arquitetura ótima da rede foi a seguinte:

Número de neurônios na primeira camada: 75.
Número de neurônios na segunda camada: 80.
Número de neurônios na terceira camada: 70.

### 4. Conclusões

Este trabalho verificou a influência de parâmetros utilizados na construção de uma rede neural do tipo LSTM nos resultados obtidos quando aplicada a previsão de preço de ações.
Variou-se todos os parâmetros de entrada e número de neurônios na arquitetura da rede para definir uma configuração ótima, que apresentasse valores mínimos de RMSE e MAPE.

Estes valores foram os seguintes:
- window = 15.
- epochs = 64.
- batch = 100.
  
A arquitetura ótima definida foi a seguinte:

- Número de neurônios na primeira camada: 75.
- Número de neurônios na segunda camada: 80.
- Número de neurônios na terceira camada: 70.
  
Para esta configuração ótima os valores de RMSE e MAPE otibitos foram 1.096 e 3.105, respectivamente. 

Adicionalmente, as demais métricas de avaliação obtidas nesta análise foram:
- MSE: 1.201.
- R2: 0.951.
- R2 adj: 0.951.
- 
Cabe ressaltar ainda que também foi elaborado um estudo com redes neurais do tipo GRU, mas os resultados foram bastante insatisfatórios quando comparados aos obtidos pelo uso de LSTM.

---

Matrícula: 192.671.071

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
