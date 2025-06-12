# 📁 Sobre o Projeto  
Tipo: Classificação binária  

Modelo principal: Regressão Logística e XGBoost  

Balanceamento: SMOTE (oversampling)  

Fonte dos dados: Telco Customer Churn - https://www.kaggle.com/datasets/blastchar/telco-customer-churn  

Ferramentas utilizadas:  

Python (Pandas, NumPy, Seaborn, Scikit-learn, XGBoost)  

SQLite  

Visualização com Matplotlib e Seaborn  

# 📊 Etapas do Projeto  
1. Entendimento e Coleta dos Dados  
        Conexão com banco de dados SQLite  

        Leitura da tabela Churn  

        Verificação de duplicatas e valores ausentes  

2. Análise Exploratória de Dados (EDA)  
        Análise de distribuições com histograma (usando regra de Freedman-Diaconis)  

       Verificação de assimetrias  

2.1 Análises estatísticas:  
      Teste ne normalidade com o teste de D'Agostino Pearson
      
      Teste de Mann-Whitney  

      Qui-quadrado  

      V de Cramer  

      Correlação de Spearman  

3. Pré-processamento  
      Conversão de colunas numéricas e categóricas  

      Codificação com OneHotEncoder  

      Padronização com StandardScaler  

      Balanceamento com SMOTE para tratar desbalanceamento entre classes  

4. Modelagem  
      Separação entre treino e teste  

4.1 Treinamento dos seguintes modelos:  

      Regressão Logística  

      XGBoost Classifier  

      Busca de hiperparâmetros com GridSearchCV  

5. Avaliação  
      Matriz de confusão  

      Métricas: Precisão, Recall, F1-Score  

      AUC-ROC  

      Curva Precision-Recall  

# 📌 Principais Resultados  
Modelos foram capazes de identificar clientes propensos ao churn com boa performance.  

O modelo com melhor desempenho foi a Regressão Logística, com alta AUC e bom recall.  

O balanceamento com SMOTE ajudou a melhorar significativamente o recall, bem como a seleção de um novo limiar (threshold).  

# 📁 Arquivos  
churn.ipynb: Notebook Jupyter com toda a análise e trabalho de machine learning    

dataset.csv: Conjunto de dados original (Kaggle) 

churn.db: Banco de dados  

schema.sql: Esquema do banco de dados 

README.md: Este arquivo  
