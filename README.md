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

- Introdução

- Descrição dos Dados

- Modelos

- Resultados

- Discussão

- Conclusão

- Apêndices

Inicialmente, descrevemos o problema e o pré-processamento dos dados. Em seguida, detalhamos a especificação dos modelos em Stan, justificamos as escolhas de verossimilhança e priors, e avaliamos o desempenho por meio de diagnósticos de convergência, verificações preditivas, comparação de modelos e análise de sensibilidade. Por fim, discutimos limitações e possíveis melhorias, e incluímos os códigos completos dos modelos.

## Descrição dos Dados

O conjunto de dados foi obtido na plataforma Kaggle e contém 1.000 observações com 20 atributos categóricos, originalmente organizados pelo Prof. Hofmann. Cada entrada representa uma pessoa que contratou um empréstimo, classificada como tendo risco de crédito bom ou ruim.

O dataset completo está disponível em:

https://www.kaggle.com/datasets/kabure/german-credit-data-with-risk

9 variáveis explicativas

1 variável resposta

## Variáveis Explicativas

| Variável | Tipo | Descrição |
|----------|------|-----------|
| Age | Numérica | Idade do indivíduo |
| Duration | Numérica | Prazo do empréstimo (meses) |
| Credit_amount | Numérica | Valor do crédito |
| Sex | Categórica | Gênero (male ou female) |
| Job | Categórica | Nível de ocupação (0 a 3) |
| Housing | Categórica | Tipo de moradia (own, rent, free) |
| Saving_accounts | Categórica | Nível de recursos na poupança |
| Checking_account | Categórica | Nível de recursos na conta corrente |
| Purpose | Categórica | Finalidade do empréstimo |

## Variável Resposta

| Variável | Tipo | Descrição |
|----------|------|-----------|
| Risk | Categórica | Classificação de risco (good = bom, bad = ruim) |
