# Desafio de Análise de Dados: Evasão de Clientes (Churn) da Telecom X

**Challenge ONE - Oracle Next Education + Alura**

*Autor: Anderson Machado.*

## 1. Propósito da Análise (O Problema de Negócio)

A empresa de telecomunicações "Telecom X" está enfrentando uma alta taxa de evasão de clientes (churn), mas não possui uma compreensão clara sobre os principais motivos que levam a esses cancelamentos.

O objetivo deste projeto é realizar um processo completo de **ETL (Extração, Transformação e Carregamento)** e uma **Análise Exploratória de Dados (EDA)** sobre a base de clientes da empresa. A finalidade é identificar os padrões e o perfil dos clientes com maior propensão ao churn, gerando insights que possam subsidiar a criação de estratégias de negócio focadas na retenção e fidelização de clientes.

## 2. Ferramentas Utilizadas
* Python
* Bibliotecas:
    * Pandas
    * Requests
    * Matplotlib
    * Seaborn
* Git & GitHub para versionamento
* Google Colab como ambiente de desenvolvimento

## 3. Processo de ETL
O processo de ETL foi realizado para garantir a qualidade e a consistência dos dados antes da análise. As principais etapas foram:
* **Extração (Extract):** Os dados foram extraídos via requisição HTTP de uma API que retornava um arquivo no formato JSON Lines, hospedado em um repositório do GitHub.
* **Transformação (Transform):**
    1.  Os dados JSON aninhados foram normalizados ("achatados") para um formato tabular utilizando a função `pandas.json_normalize`.
    2.  Foi identificado e corrigido um erro de tipo de dado na coluna `account.Charges.Total`, que estava como `object` (texto) devido à presença de valores com espaços em branco. A coluna foi convertida para um tipo numérico (`float64`), e os valores problemáticos foram tratados como nulos.
    3.  Foram identificados e removidos 224 registros que possuíam um valor inválido (texto vazio) na coluna alvo `Churn`.
    4.  As 11 linhas com valores nulos resultantes na coluna `account.Charges.Total` foram removidas, por representarem uma fração insignificante do dataset (0.15%).

## 4. Análise Exploratória (EDA): Principais Gráficos e Insights

*(Lembre-se de substituir `nome_do_arquivo.png` pelos nomes exatos dos seus arquivos de imagem que você subiu para o GitHub)*

### Insight 1: O Contrato Mensal e o Baixo Tempo de Serviço são os Maiores Preditores de Churn

![Gráfico de Churn por Tempo de Contrato](Análise%20de%20Churn.png)
![Gráfico de Churn por Tipo de Contrato](Distribuição%20de%20Account.png)

A análise revela que o tipo de contrato e o tempo de permanência do cliente (`tenure`) são os fatores mais impactantes. Clientes com **contrato "Mês a mês"** apresentam uma taxa de evasão drasticamente superior. Além disso, o boxplot mostra que a **maioria dos cancelamentos ocorre nos estágios iniciais** do ciclo de vida do cliente, com a média de `tenure` dos clientes que evadem sendo significativamente menor.

### Insight 2: Serviços de Valor Agregado Aumentam a Retenção

![Gráfico de Churn por Serviço de Segurança Online](Proporção%20de%20Churn%20Por%20Serviço.png)

Clientes que **não contratam serviços de valor agregado**, como Segurança Online (`OnlineSecurity`) e Suporte Técnico (`TechSupport`), tendem a cancelar mais. Isso sugere que esses serviços atuam como um fator de "aderência" (*stickiness*), aumentando o engajamento do cliente com o ecossistema da empresa.

### Insight 3: O Método de Pagamento e a Fatura Online Indicam Risco

![Gráfico de Churn por Tipo de Fatura](Proporção%20de%20Churn%20Por%20Account.png)

Observa-se uma taxa de churn desproporcionalmente maior entre clientes que optam pela **fatura online (`PaperlessBilling`)** e, em especial, aqueles que utilizam **cheque eletrônico** como método de pagamento. Isso pode indicar atritos na experiência de pagamento digital.

## 5. Conclusão e Sugestões Estratégicas

A análise permitiu traçar um perfil claro do cliente com alto risco de evasão, caracterizado principalmente por possuir contrato mensal, ser um cliente recente, não ter serviços de proteção e utilizar métodos de pagamento digitais específicos.

Com base nisso, as seguintes ações são recomendadas para a Telecom X:

1.  **Revisar a Estratégia para Novos Clientes:** Criar um **programa de fidelidade focado nos primeiros 6 meses**, oferecendo benefícios para a migração do plano "Mês a mês" para um contrato anual.
2.  **Fortalecer a Oferta de Serviços Agregados:** Oferecer pacotes de "Boas-vindas Digitais" com meses gratuitos de `OnlineSecurity` e `TechSupport` para novos clientes, aumentando o valor percebido e a retenção.
3.  **Investigar a Experiência de Pagamento Online:** Realizar uma **análise de usabilidade (UX) do portal de pagamento** para identificar e remover possíveis atritos, além de incentivar a migração para métodos de pagamento mais estáveis, como débito automático.

## 6. Instruções para Executar o Projeto

1.  Clone este repositório: `git clone https://github.com/AndersonPM15/desafio-analise-churn-telecom`
2.  Navegue até a pasta do projeto.
3.  As bibliotecas necessárias são: `pandas`, `requests`, `matplotlib`, `seaborn`. Caso não as tenha, instale com `pip install pandas requests matplotlib seaborn`.
4.  Abra e execute o notebook `analise_churn_telecom.ipynb` em um ambiente como Jupyter Notebook, Jupyter Lab ou Google Colab.
