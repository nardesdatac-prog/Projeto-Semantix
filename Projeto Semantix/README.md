# Projeto Semantix — Análise de Risco de Crédito

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)
![Scikit--learn](https://img.shields.io/badge/scikit--learn-Machine%20Learning-F7931E?logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-Modeling-2C3E50)
![Status](https://img.shields.io/badge/Status-Concluído-2E7D32)

Projeto desenvolvido no contexto do **Programa de Empregabilidade da EBAC**, com foco na análise de risco de crédito e identificação de padrões associados à ocorrência de inadimplência.

O projeto percorre todo o fluxo de uma análise de dados aplicada: **exploração → preparação → modelagem → avaliação**, utilizando técnicas de Estatística, Machine Learning e visualização de dados.

---

## Visão geral

O acesso ao crédito possui papel importante na vida financeira das pessoas. Ao mesmo tempo, características relacionadas ao perfil financeiro, ao empréstimo contratado e ao histórico de crédito podem estar associadas a diferentes níveis de risco de inadimplência.

A proposta deste projeto é investigar essas relações a partir de um conjunto de dados de risco de crédito, buscando compreender quais características estão associadas à ocorrência de inadimplência e avaliar a capacidade de diferentes modelos de Machine Learning em identificar esses casos.

A variável-alvo utilizada foi `loan_status`, em que:

- `0` representa um empréstimo sem inadimplência;
- `1` representa um empréstimo com inadimplência.

---

## Problemática

> **Quais características financeiras, socioeconômicas e relacionadas ao crédito estão associadas à ocorrência de inadimplência?**

A partir dessa questão, o projeto busca explorar o comportamento dos dados e comparar diferentes abordagens de modelagem para identificar padrões associados ao risco de crédito.

---

## Objetivos

### Objetivo geral

Explorar os fatores associados à ocorrência de inadimplência e avaliar diferentes modelos de Machine Learning para classificação do risco de crédito.

### Objetivos específicos

- Realizar uma análise exploratória dos dados;
- Identificar valores ausentes, extremos e possíveis inconsistências;
- Preparar as variáveis para utilização nos modelos;
- Aplicar Regressão Linear como modelo de referência;
- Comparar Decision Tree e XGBoost utilizando Cross Validation;
- Avaliar os modelos por diferentes métricas de classificação;
- Identificar o modelo com melhor desempenho geral;
- Extrair insights que contribuam para a compreensão do risco de inadimplência.

---

## Dataset

O projeto utiliza um conjunto de dados público de **Credit Risk**, contendo informações relacionadas ao perfil dos clientes, características dos empréstimos e histórico de crédito.

A base possui informações como:

| Variável | Descrição |
|---|---|
| `person_age` | Idade do cliente |
| `person_income` | Renda anual |
| `person_home_ownership` | Tipo de propriedade/moradia |
| `person_emp_length` | Tempo de emprego em anos |
| `loan_intent` | Finalidade do empréstimo |
| `loan_grade` | Classificação do empréstimo |
| `loan_amnt` | Valor do empréstimo |
| `loan_int_rate` | Taxa de juros |
| `loan_status` | Indicador de inadimplência |
| `loan_percent_income` | Percentual da renda comprometido com o empréstimo |
| `cb_person_default_on_file` | Histórico de inadimplência registrado |
| `cb_person_cred_hist_length` | Tempo de histórico de crédito |

A variável `loan_status` foi utilizada como variável-alvo dos modelos de classificação.

---

## Metodologia

O projeto foi estruturado em quatro etapas principais.

### 1. Exploração dos dados

Arquivo: `notebooks/01_exploracao.ipynb`

Nesta etapa foram analisados:

- estrutura e tipos das variáveis;
- valores ausentes;
- estatísticas descritivas;
- distribuição das variáveis numéricas;
- distribuição das variáveis categóricas;
- distribuição da variável-alvo;
- possíveis valores extremos.

Entre os principais pontos identificados estavam valores extremos em idade e tempo de emprego, forte assimetria em renda e valores ausentes em `person_emp_length` e `loan_int_rate`.

---

### 2. Preparação dos dados

Arquivo: `notebooks/02_preparacao.ipynb`

Os dados foram preparados para utilização nos modelos.

Principais procedimentos:

- preenchimento dos valores ausentes pela mediana;
- tratamento de valores extremos incompatíveis com o contexto;
- transformação das variáveis categóricas;
- codificação ordinal de `loan_grade`;
- transformação binária de `cb_person_default_on_file`;
- aplicação de One-Hot Encoding em variáveis categóricas sem ordem;
- separação entre preditores (`X`) e variável-alvo (`y`);
- divisão entre treino e teste;
- estratificação pela variável-alvo.

A divisão utilizada foi de **80% para treinamento e 20% para teste**, com `random_state=42`.

Os conjuntos preparados foram salvos em `data/` para manter a separação entre as etapas do projeto.

---

### 3. Modelagem

Arquivo: `notebooks/03_modelagem.ipynb`

Foram utilizados três modelos:

#### Regressão Linear

Utilizada como modelo de referência. Embora seja tradicionalmente destinada a problemas de regressão, foi incluída para atender à proposta do projeto e demonstrar suas limitações quando aplicada a uma variável-alvo binária.

#### Decision Tree

Modelo de classificação baseado em árvores de decisão, capaz de representar relações não lineares entre as características dos clientes e a ocorrência de inadimplência.

#### XGBoost

Modelo baseado em boosting, utilizado para comparar uma abordagem mais robusta de aprendizado de máquina com a árvore de decisão.

### Cross Validation

Decision Tree e XGBoost foram comparados utilizando **Cross Validation com 5 folds** e acurácia como métrica inicial.

Resultados médios:

| Modelo | Acurácia média |
|---|---:|
| Decision Tree | 89,26% |
| XGBoost | 93,60% |

O XGBoost apresentou melhor desempenho médio durante a validação cruzada.

---

## Avaliação dos modelos

Arquivo: `notebooks/04_avaliacao.ipynb`

Após o treinamento, os modelos foram avaliados no conjunto de teste.

Foram utilizadas:

- Acurácia;
- Precisão;
- Recall;
- F1-score;
- Matriz de confusão;
- ROC-AUC;
- Classification Report.

Essas métricas permitem observar não apenas a quantidade geral de acertos, mas também como os modelos se comportam especificamente na identificação dos casos de inadimplência.

---

## Resultados

### Comparação final

| Modelo | Acurácia | Precisão | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Regressão Linear | 84,65% | 77,73% | 41,52% | 54,13% | 85,40% |
| Decision Tree | 88,44% | 72,06% | **76,78%** | 74,34% | 84,24% |
| XGBoost | **93,38%** | **96,00%** | 72,70% | **82,74%** | **95,03%** |

### Interpretação

O **XGBoost apresentou o melhor desempenho geral** entre os modelos avaliados.

O modelo alcançou:

- **93,38% de acurácia**;
- **96,00% de precisão**;
- **82,74% de F1-score**;
- **95,03% de ROC-AUC**.

A Decision Tree apresentou um **recall de 76,78%**, superior ao XGBoost. Isso significa que conseguiu identificar uma parcela ligeiramente maior dos casos reais de inadimplência.

Por outro lado, a Decision Tree apresentou precisão de 72,06%, enquanto o XGBoost alcançou 96,00%. A matriz de confusão também mostrou uma diferença importante:

| Modelo | Verdadeiros negativos | Falsos positivos | Falsos negativos | Verdadeiros positivos |
|---|---:|---:|---:|---:|
| Regressão Linear | 4.925 | 169 | 831 | 590 |
| Decision Tree | 4.671 | 423 | 330 | 1.091 |
| XGBoost | **5.051** | **43** | 388 | 1.033 |

O XGBoost apresentou apenas **43 falsos positivos**, enquanto a Decision Tree apresentou 423. Ao mesmo tempo, identificou 1.033 dos 1.421 casos reais de inadimplência presentes no conjunto de teste.

Assim, embora a Decision Tree tenha apresentado vantagem específica no recall, o XGBoost apresentou o melhor equilíbrio geral entre precisão, F1-score, capacidade de discriminação e acurácia.

---

## Principais insights

A análise permitiu observar alguns pontos relevantes:

1. O conjunto apresenta uma distribuição desigual entre as classes de `loan_status`, com predominância de registros sem inadimplência.

2. Variáveis financeiras como renda, valor do empréstimo, taxa de juros e comprometimento da renda apresentam distribuições assimétricas e valores extremos, exigindo atenção durante a preparação dos dados.

3. A Regressão Linear apresentou limitações para o problema de classificação, principalmente na identificação da classe de inadimplência.

4. A Decision Tree apresentou maior capacidade de identificar inadimplentes do que o XGBoost, mas gerou uma quantidade significativamente maior de falsos positivos.

5. O XGBoost apresentou o melhor desempenho geral, com destaque para precisão, F1-score e ROC-AUC.

6. A comparação entre métricas demonstra que a escolha de um modelo não deve considerar apenas a acurácia. Diferentes métricas revelam diferentes tipos de erro e capacidades de classificação.

---

## Conclusão

A análise demonstrou que características relacionadas ao perfil financeiro, ao empréstimo e ao histórico de crédito podem ser utilizadas para investigar padrões associados à inadimplência.

Entre os modelos avaliados, o **XGBoost apresentou o desempenho geral mais consistente**, alcançando 93,38% de acurácia, 96,00% de precisão, 82,74% de F1-score e 95,03% de ROC-AUC.

Apesar de a Decision Tree apresentar recall superior para a classe de inadimplência, o XGBoost apresentou uma quantidade muito menor de falsos positivos e melhor equilíbrio entre as principais métricas.

Dessa forma, considerando o conjunto de dados e a metodologia utilizada neste projeto, o **XGBoost foi selecionado como o modelo de melhor desempenho**.

É importante destacar que os resultados representam o comportamento observado neste conjunto de dados e não devem ser interpretados como uma ferramenta pronta para decisões reais de concessão de crédito. Em um cenário de produção, seriam necessários dados mais abrangentes, validações adicionais, análise de viés, monitoramento do modelo e avaliação do impacto dos erros de classificação.

---

## Estrutura do projeto

```text
Projeto Semantix/
│
├── data/
│   ├── credit_risk_dataset.csv
│   ├── X_train.csv
│   ├── X_test.csv
│   ├── y_train.csv
│   └── y_test.csv
│
├── notebooks/
│   ├── 01_exploracao.ipynb
│   ├── 02_preparacao.ipynb
│   ├── 03_modelagem.ipynb
│   └── 04_avaliacao.ipynb
│
├── reports/
│   └── figures/
│
├── src/
│   ├── __init__.py
│   ├── data_processing.py
│   └── visualization.py
│
├── README.md
└── requirements.txt
```

A organização separa as diferentes fases do projeto, facilitando a leitura, manutenção e reutilização do trabalho.

---

## Tecnologias e bibliotecas

O projeto foi desenvolvido em Python utilizando principalmente:

- **Python** — linguagem utilizada no desenvolvimento;
- **Pandas** — manipulação e análise dos dados;
- **NumPy** — operações numéricas;
- **Matplotlib** — visualização de dados;
- **Seaborn** — visualização estatística;
- **Scikit-learn** — preparação, validação e avaliação dos modelos;
- **XGBoost** — modelo de Machine Learning baseado em boosting;
- **Jupyter Notebook** — desenvolvimento e documentação das etapas.

---

## Como executar

Clone o repositório:

```bash
git clone SEU_LINK_DO_REPOSITORIO
```

Entre na pasta:

```bash
cd "Projeto Semantix"
```

Instale as dependências:

```bash
pip install -r requirements.txt
```

Depois, execute os notebooks na seguinte ordem:

```text
01_exploracao.ipynb
        ↓
02_preparacao.ipynb
        ↓
03_modelagem.ipynb
        ↓
04_avaliacao.ipynb
```

A ordem é importante porque cada etapa utiliza os resultados produzidos anteriormente.

---

## Possibilidades de evolução

Como continuidade do projeto, algumas possibilidades seriam:

- testar técnicas específicas para lidar com o desbalanceamento das classes;
- realizar otimização dos hiperparâmetros do XGBoost;
- comparar diferentes estratégias de seleção de variáveis;
- avaliar outras métricas, como Precision-Recall AUC;
- analisar a importância das variáveis;
- investigar a interpretabilidade das previsões;
- testar o comportamento do modelo em novos conjuntos de dados;
- desenvolver uma visualização interativa dos resultados.

Essas possibilidades não fazem parte da avaliação atual e são apresentadas como caminhos para evolução futura do projeto.

---

## Contexto acadêmico

Projeto desenvolvido como parte da formação em **Ciência de Dados pela EBAC — Escola Britânica de Artes Criativas e Tecnologia**, no contexto do **Projeto Semantix**.

O projeto foi desenvolvido com foco na aplicação prática dos conhecimentos adquiridos ao longo da formação, integrando análise exploratória, preparação de dados, estatística, Machine Learning, validação e avaliação de modelos.

---

## Autor

**A. Nardes**

Projeto desenvolvido para fins acadêmicos e de portfólio em Ciência de Dados.

[GitHub](https://github.com/nardesdatac-prog)
