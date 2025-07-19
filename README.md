# Combate-as-fraudes

# Projeto: Detecção de Fraudes em Transações Financeiras

## 🚀 Visão Geral

Este projeto visa desenvolver um modelo de Machine Learning capaz de identificar transações financeiras fraudulentas utilizando um dataset sintético que simula dados reais de transações com cartão de crédito. O trabalho aborda desafios comuns em problemas de detecção de fraude, como o desbalanceamento de classes e a necessidade de otimizar métricas específicas como Recall e Precision.

## 🎯 Objetivo

O principal objetivo é construir um modelo preditivo que minimize as perdas financeiras causadas por fraudes (maximizando o Recall) sem gerar um volume excessivo de falsos alertas (controlando os Falsos Positivos), garantindo a aplicabilidade em um ambiente de produção.

## 📊 Dataset

O dataset utilizado contém transações anonimizadas, onde as features `V1` a `V28` são os principais componentes obtidos via PCA. Além disso, as colunas `Time` (tempo decorrido desde a primeira transação) e `Amount` (valor da transação) são fornecidas. A variável alvo é `Class` (0 para legítima, 1 para fraude).

## 🔑 Principais Descobertas e Etapas

1.  **Análise Exploratória de Dados (EDA):**
    * Identificação de **desbalanceamento extremo de classes** (`Class=1` representa apenas 0.17% das transações).
    * Análise da variável `Time` e criação da feature `Hour`, revelando concentração de fraudes nas **horas da madrugada (1h-4h)**.
    * Análise da distribuição de `Amount`, destacando que o **maior impacto financeiro das fraudes** está em transações de alto valor, apesar da maioria das fraudes ser de baixo valor.
    * Utilização de **KDE plots** e análise de correlação para identificar variáveis `V` com alto poder discriminatório (e.g., V11, V12, V14, V17).

2.  **Pré-processamento e Balanceamento de Classes:**
    * Divisão estratificada dos dados em treino e teste (`train_test_split`).
    * Aplicação de **SMOTE** (Synthetic Minority Over-sampling Technique) no conjunto de treino para balancear a classe minoritária, crucial para o aprendizado do modelo.

3.  **Modelagem e Avaliação de Modelos:**
    * Comparação de diversos algoritmos (Regressão Logística, Random Forest, XGBoost).
    * O **XGBoost**, treinado com dados balanceados por SMOTE, foi o modelo escolhido por oferecer o melhor equilíbrio entre Recall e Precision.
    * **Resultados Finais do Modelo XGBoost (Otimizado):**
        ```
        Matriz de Confusão:
        [[56794    70]
         [   14    84]]

        Classification Report:
                      precision    recall  f1-score   support

                   0       1.00      1.00      1.00     56864
                   1       0.55      0.86      0.67        98

            accuracy                           1.00     56962
           macro avg       0.77      0.93      0.83     56962
        weighted avg       1.00      1.00      1.00     56962

        AUC-ROC: 0.9784227386790394
        ```
    * **Otimização de Hiperparâmetros:** Foi realizada uma busca com `RandomizedSearchCV` para otimizar os hiperparâmetros do XGBoost. Embora a otimização não tenha resultado em ganhos substanciais de performance (o modelo já era robusto), ela validou a escolha dos parâmetros próximos aos padrões.

4.  **Análise de Erros e Limiar de Decisão:**
    * A **curva Precision-Recall vs. Threshold** foi plotada para visualizar o trade-off entre Precisão e Recall em diferentes limiares.
    * Análise dos **14 Falsos Negativos** (fraudes não detectadas) e **70 Falsos Positivos** (alertas errados), revelando que transações de baixo valor e a ausência de padrões temporais muito específicos podem ser pontos de dificuldade para o modelo.

## 🛠 Tecnologias Utilizadas

* `Python`
* `Pandas`
* `NumPy`
* `Matplotlib`
* `Seaborn`
* `Scikit-learn`
* `XGBoost`
* `Imbalanced-learn` (para SMOTE)

## 🚀 Como Executar o Projeto

1.  Clone este repositório:
    ```bash
    git clone [https://github.com/](https://github.com/)[Seu-Usuario]/[Nome-do-Seu-Repositorio].git
    ```
2.  Navegue até o diretório do projeto:
    ```bash
    cd [Nome-do-Seu-Repositorio]
    ```
3.  Crie e ative um ambiente virtual (recomendado):
    ```bash
    python -m venv venv
    source venv/bin/activate  # Linux/macOS
    .\venv\Scripts\activate   # Windows
    ```
4.  Instale as dependências:
    ```bash
    pip install -r requirements.txt
    ```
    (Você precisará criar um arquivo `requirements.txt` com `pip freeze > requirements.txt` no seu ambiente com as bibliotecas instaladas)
5.  Abra e execute o notebook Jupyter:
    ```bash
    jupyter notebook
    ```
    O notebook principal é `[Nome-do-Seu-Notebook.ipynb]`.

## 🤝 Contribuições

Sinta-se à vontade para abrir issues ou pull requests se tiver sugestões ou melhorias!

## 📧 Contato

JONATHAN CARVALHO
https://www.linkedin.com/in/jonathan-datascience/
