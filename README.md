# Projeto de Previsão de Churn de Clientes 📉


## 📁 Sobre o Projeto

Este projeto foca na **previsão de comportamento de clientes** para identificar aqueles propensos a cancelar seus serviços (churn). Utilizando técnicas de Machine Learning, o objetivo é analisar dados relevantes dos clientes e desenvolver um modelo capaz de auxiliar na criação de programas de retenção focados.

* **Tipo de Problema**: Classificação Binária (Churn ou Não Churn)
* **Modelo Principal**: Regressão Logística Otimizada (melhor desempenho para o objetivo) e outros modelos explorados (XGBoost Classifier, Random Forest Classifier, LightGBM Classifier).
* **Técnica de Balanceamento**: SMOTE (Synthetic Minority Over-sampling Technique) para lidar com o desbalanceamento de classes.
* **Fonte dos Dados**: [Telco Customer Churn - Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
* **Ferramentas Utilizadas**:
    * **Python**:
        * `Pandas`: Manipulação e análise de dados.
        * `NumPy`: Operações numéricas.
        * `Matplotlib` e `Seaborn`: Visualização de dados.
        * `Scikit-learn`: Pré-processamento, modelagem (Regressão Logística), avaliação e busca de hiperparâmetros (GridSearchCV).
        * `XGBoost`: Modelo de classificação.
    * **SQLite**: Gerenciamento e consulta do banco de dados local.
    * **Jupyter Notebook**: Ambiente de desenvolvimento e execução do código.

## 📊 Etapas do Projeto

O desenvolvimento deste projeto seguiu as seguintes etapas:

### 1. Entendimento e Coleta dos Dados
Nesta fase inicial, o foco foi compreender a estrutura dos dados e garantir sua qualidade.
* Conexão com o banco de dados SQLite (`churn.db`).
* Leitura e carregamento da tabela `Churn` para um DataFrame do Pandas.
* Verificação de duplicatas e tratamento de valores ausentes, garantindo a integridade do dataset.

### 2. Análise Exploratória de Dados (EDA)
A EDA permitiu obter insights sobre as distribuições das variáveis e suas relações com o churn.
* Análise de distribuições de variáveis numéricas com histogramas, utilizando a regra de Freedman-Diaconis para otimização do número de bins.
* Verificação da assimetria das distribuições para identificar a necessidade de transformações.

#### 2.1 Análises Estatísticas

Foram aplicados diversos testes estatísticos para avaliar a associação e correlação entre as features e a variável alvo (`Churn`).
* **Teste de Normalidade**: Teste de D'Agostino-Pearson para verificar a normalidade das distribuições numéricas.
* **Teste de Mann-Whitney U**: Comparação de grupos para variáveis numéricas e binárias (Churn).
* **Teste de Qui-quadrado (Chi-squared)**: Avaliação da associação entre variáveis categóricas.
* **V de Cramer**: Medida da força de associação entre variáveis categóricas.
* **Correlação de Spearman**: Avaliação da correlação entre variáveis numéricas (útil para relações não lineares).

### 3. Pré-processamento
Preparação dos dados para a modelagem, garantindo que estejam no formato adequado para os algoritmos de Machine Learning.
* Conversão de colunas numéricas (como `TotalCharges`) que poderiam ter sido interpretadas como texto.
* Codificação de variáveis categóricas com `OneHotEncoder`, transformando-as em formato numérico.
* Padronização de variáveis numéricas com `StandardScaler`, colocando-as na mesma escala.
* Balanceamento das classes de churn com `SMOTE` (Synthetic Minority Over-sampling Technique) para lidar com o desbalanceamento natural do dataset, melhorando o desempenho do modelo na classe minoritária.

### 4. Modelagem
Construção e otimização dos modelos de previsão.
* Separação dos dados em conjuntos de treino e teste para validação do modelo.
* **Treinamento dos seguintes modelos de classificação**:
    * Regressão Logística
    * XGBoost Classifier
* **Busca de Hiperparâmetros**: Utilização de `GridSearchCV` para otimizar os hiperparâmetros dos modelos.

### 5. Avaliação
Análise detalhada do desempenho de cada modelo.
* **Matriz de Confusão**: Visualização dos Verdadeiros Positivos, Verdadeiros Negativos, Falsos Positivos e Falsos Negativos.
* **Métricas de Classificação**: Avaliação com Precisão (`Precision`), Recall (Sensibilidade), F1-Score e Acurácia (`Accuracy`).
* **AUC-ROC (Area Under the Receiver Operating Characteristic Curve)**: Métrica robusta para avaliação em datasets desbalanceados.
* **Curva Precision-Recall**: Análise visual do trade-off entre Precisão e Recall em diferentes limiares de decisão.
* **Ajuste de Limiar (Threshold)**: Otimização do limiar de probabilidade da Regressão Logística para maximizar o Recall, alinhando o modelo ao objetivo de negócio de retenção.

## 📌 Principais Resultados e Insights

A análise dos modelos revelou que o problema de churn é desafiador devido ao desbalanceamento de classes, mas os modelos foram capazes de identificar clientes propensos ao churn com boa performance.

* **Destaque da Regressão Logística**: Este modelo apresentou o melhor desempenho geral, especialmente em métricas críticas para a retenção de clientes:
    * **Alto Recall (Sensibilidade)**: Com um Recall de **0.90**, o modelo conseguiu identificar 90% dos clientes que *realmente* cancelaram seus serviços. Isso é crucial para um programa de retenção, que visa intervir proativamente.
    * O balanceamento com **SMOTE** foi fundamental para a melhoria significativa do Recall, e o ajuste do **limiar de decisão (threshold)** da Regressão Logística permitiu um controle ainda maior sobre o trade-off entre Precisão e Recall, priorizando a identificação de clientes em risco.

* **Fatores Chave que Influenciam o Churn (Baseado na análise da Regressão Logística - os coeficientes do modelo indicariam a direção e magnitude da influência)**:
    * Serviço de Internet (`InternetService`)
    * Segurança Online (`OnlineSecurity`)
    * Backup Online (`OnlineBackup`)
    * Proteção de Dispositivo (`DeviceProtection`)
    * Suporte Técnico (`TechSupport`)
    * Serviço de Streaming de TV (`StreamingTV`)
    * Serviço de Streaming de Filmes (`StreamingMovies`)
    * Tipo de Contrato (`Contract`)
    * Método de Pagamento (`PaymentMethod`)
    * Tempo de Cliente (`Tenure`)
    * Total de Gastos (`TotalCharges`)

## 📁 Arquivos

* `churn.ipynb`: Notebook Jupyter contendo toda a análise exploratória de dados, pré-processamento, treinamento e avaliação dos modelos de Machine Learning.
* `dataset.csv`: O conjunto de dados original utilizado no projeto, obtido do Kaggle.
* `churn.db`: Banco de dados SQLite contendo a tabela de churn.
* `schema.sql`: O esquema SQL do banco de dados.
* `README.md`: Este arquivo, detalhando o projeto.
