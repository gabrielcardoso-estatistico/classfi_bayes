# Análise do Risco de Crédito por Meio de Modelos Bayesianos de Regressão Logística

Análise de risco de crédito utilizando modelos de Regressão Logística pooled e hierárquica.


Autor: Gabriel Cardoso

## Introdução

Um dos serviços mais importantes oferecidos pelos bancos — e que atrai os clientes — é a concessão de crédito. No entanto, ao oferecerem empréstimos imobiliários, financiamentos de veículos ou crédito empresarial, as instituições financeiras estão expostas ao risco de inadimplência dos tomadores, conhecido como risco de crédito. Esse risco refere-se à possibilidade de perda para o credor devido à incapacidade do devedor de honrar suas obrigações. Quando mal gerenciado, o risco de crédito pode ter consequências graves, como ilustrado pela crise financeira de 2008, que levou o sistema bancário à beira do colapso.

Diante disso, é fundamental avaliar a capacidade de pagamento dos tomadores e os riscos envolvidos — processo conhecido como análise de risco de crédito. Este tema foi escolhido pela sua relevância prática e pela escassez de projetos de análise de dados que aplicam métodos bayesianos a problemas de crédito.

O objetivo deste trabalho é utilizar Regressão Logística para classificar empréstimos como “bons” ou “ruins”, empregando dois modelos:

- Um modelo pooled (agrupado)

- Um modelo hierárquico

A comparação entre eles permitirá identificar qual apresenta melhor desempenho para a tarefa proposta.

O relatório está organizado da seguinte forma:

Introdução

Descrição dos Dados

Modelos

Resultados

Discussão

Conclusão

Apêndices

Inicialmente, descrevemos o problema e o pré-processamento dos dados. Em seguida, detalhamos a especificação dos modelos em Stan, justificamos as escolhas de verossimilhança e priors, e avaliamos o desempenho por meio de diagnósticos de convergência, verificações preditivas, comparação de modelos e análise de sensibilidade. Por fim, discutimos limitações e possíveis melhorias, e incluímos os códigos completos dos modelos.

Descrição dos Dados
O conjunto de dados foi obtido na plataforma Kaggle e contém 1.000 observações com 20 atributos categóricos, originalmente organizados pelo Prof. Hofmann. Cada entrada representa uma pessoa que contratou um empréstimo, classificada como tendo risco de crédito bom ou ruim.

O dataset completo está disponível em:

## Data description
The data set is obtained through Kaggle. It contains 1000 data points with 20 categorical attributes created by Professor Hofmann. In this data set, each entry represents a person taking credit from a bank, and each person is classified as having good or bad credit risk according to the set of attributes. The full data set can be found [here](https://www.kaggle.com/datasets/kabure/german-credit-data-with-risk).

The data consists of 10 columns, 9 explanatory variables, and 1 target variable, defined as follows:

Explanatory variables:

- Age (numerical/continuous): The age of the subject.
- Duration (numerical/continuous): The contracted loan due time (in months).
- Credit.amount (numerical/continuous): The amount of credit of the subject's loan.
- Sex (textual/categorical): The gender of the subject. This includes "`male`" and "`female`".
- Job (numerical/categorical): The level of employment of the subject. This includes "`0`" - unskilled and non-resident, "`1`" - unskilled and resident, "`2`" - skilled, "`3`" - highly skilled.
- Housing (textual/categorical): The type of housing of the subject. This includes "`own`", "`rent`" and "`free`".
- Saving.accounts (textual/categorical): The level of wealth of subject's saving account. This includes "`little`", "`moderate`", "`quite rich`", "`rich`".
- Checking.account (textual/categorical): The level of wealth of subject's checking account. This includes "`little`", "`moderate`", "`quite rich`", "`rich`".
- Purpose (textual/categorical): The purpose of the subject's loan. This includes "`business`", "`car`", "`domestic appliances`", "`education`", "`furniture/equipemt`", "`radio/TV`", "`repairs`", "`vacation/others`".

Target variable:


- Risk (textual/categorical): The fact that the subject has defaulted (not repaying the loan). This includes "`good`" - good loan (the subject has repaid on time), "`bad`" - bad loan (the subject has defaulted).
