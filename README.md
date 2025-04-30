# Case PS Inteli Academy - Predição de Churn

&emsp;Este projeto tem como objetivo desenvolver um modelo de aprendizado de máquina para prever a rotatividade (churn) de clientes de uma empresa fictícia de telecomunicações, a TelecomPlus. A previsão do churn permite a empresa agir proativamente para reter clientes e minimizar perdas.

## Objetivos

- Identificar clientes com maior risco de cancelamento.

- Utilizar técnicas de processamento de dados para preparar, explorar e modelar os dados.

- Aplicar múltiplos modelos de classificação com validação cruzada e tuning de hiperparâmetros.

## Etapas do Desenvolvimento

### 1. Carregamento e Exploração Inicial

&emsp;Foram carregados os conjuntos dados_clientes.csv (dados rotulados para treino) e desafio.csv (dados sem rótulo para predição).

&emsp;A variável alvo é churn, que indica se o cliente cancelou (1) ou permaneceu (0).

&emsp;Foi realizada a inspeção inicial com info(), head() e contagem de valores da variável churn para entender distribuições e identificar valores ausentes.

### 2. Engenharia de Features

&emsp;As variáveis foram divididas por tipo: numéricas contínuas, numéricas de contagem, categóricas nominais e categóricas ordinais.

&emsp;A coluna produtos_assinados foi transformada em uma lista de produtos por cliente.

&emsp;Os 6 produtos mais frequentes foram identificados e transformados em colunas binárias indicativas para cada cliente.

### 3. Pré-processamento dos Dados

&emsp;Foi montado um pipeline usando Pipeline e ColumnTransformer para tratar os diferentes tipos de variáveis.

&emsp;Numéricos com skew: imputados com a mediana, transformados com log1p e padronizados.

&emsp;Numéricos de contagem: imputados e escalados com RobustScaler.

&emsp;Categóricos nominais: preenchidos com "missing" e codificados com One-Hot.

&emsp;Categóricos ordinais: codificados com OrdinalEncoder segundo a ordem lógica de renda.

&emsp;Produtos: considerados como variáveis já binárias (pass-through).

### 4. Modelagem Inicial

&emsp;Separaram-se os dados em X (features) e y (churn).

&emsp;Foi aplicada uma divisão treino/validação (80/20).

&emsp;O modelo RandomForestClassifier foi treinado e avaliado com accuracy_score e classification_report.

&emsp;As features mais influentes foram extraídas com base na importância atribuída pela Random Forest.

&emsp;**As features mais influentes**

![alt text](<Features mais influentes.jpg>)

### 5. Comparativo com Vários Modelos

- Foram comparados os seguintes modelos:

- Logistic Regression

- Random Forest

- XGBoost

- Gradient Boosting

- K-Nearest Neighbors

- Support Vector Machine (SVM)

- Decision Tree

&emsp;Cada modelo foi avaliado com cross_val_score (validação cruzada 5-fold).

&emsp;O Gradient Boosting obteve o melhor resultado inicial com acurácia média de aproximadamente 71,95%.

### 6. Rebalanceamento e Ajuste de Hiperparâmetros

&emsp;Apesar de resultado já ser maior que 70%, não foi tão satisfatório. Então foi aplicado SMOTE para rebalancear as classes (a variável churn estava desbalanceada).

&emsp;Utilizou-se GridSearchCV para ajustar os hiperparâmetros de:

- Gradient Boosting

- Random Forest

- XGBoost

&emsp;O melhor modelo foi selecionado automaticamente com base na média da acurácia dos folds.

&emsp;O modelo escolhido foi treinado com os dados balanceados e aplicados ao conjunto desafio.csv.

## Resultados

&emsp;Melhor acurácia obtida com modelos balanceados e tunados: = 79,05%.

&emsp;Geração do arquivo final resultado_Kaio.csv com as previsões de churn para os clientes no conjunto de teste.

### 1. Tecnologias Utilizadas

&emsp;Python 3.11

&emsp;Pandas, Numpy, Scikit-learn, XGBoost, Imbalanced-learn

&emsp; Google Colab

### 2. Como Executar

&emsp;De preferência use Google Colab

&emsp;Execute as células do notebook na ordem.

&emsp;Ao final, o arquivo resultado_tunado_seu_nome.csv será gerado automaticamente com as previsões.

### 3. Possíveis Melhorias Futuras

&emsp;Aplicar LightGBM e CatBoost.

&emsp;Utilizar outras métricas de avaliação (ROC AUC, recall).

&emsp;Melhorar ainda mais os hiperparâmetros e fazer uma seleção ainda mais precisa dos dados de entrada.