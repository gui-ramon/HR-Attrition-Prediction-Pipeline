# 🎯 HR Attrition Prediction Pipeline

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Machine Learning](https://img.shields.io/badge/Machine%20Learning-HR%20Analytics-green)](https://github.com/matheuspavanids/project-ml-mackenzie)

## 📋 Visão Geral

Sistema completo de Machine Learning para previsão de rotatividade (attrition) de funcionários, desenvolvido como projeto acadêmico para o Mackenzie. O pipeline implementa técnicas avançadas de balanceamento de dados, otimização de hiperparâmetros e múltiplos algoritmos de classificação.

### 🎯 Objetivos do Projeto

- Prever com alta precisão quais funcionários têm maior probabilidade de deixar a empresa
- Identificar os principais fatores que contribuem para a rotatividade
- Fornecer insights acionáveis para o departamento de RH
- Demonstrar técnicas avançadas de tratamento de dados desbalanceados

### 📊 Resultados Principais

- **Melhor Modelo**: LightGBM
- **F1-Score**: 0.3672 (LightGBM)
- **Recall**: 0.5120 (capacidade de identificar funcionários em risco)
- **AUC-ROC**: 0.6751
- **Dataset**: 1.000.000 registros sintéticos baseados no padrão IBM HR Analytics

## 🚀 Funcionalidades

### 1. **Pipeline Completo de ML**
- Preparação automática de dados
- Feature engineering avançado (53 features selecionados)
- Múltiplos modelos: Random Forest, Logistic Regression, LightGBM, Rigde Classifier
- Otimização automática de hiperparâmetros com Optuna

### 2. **Tratamento de Desbalanceamento**
- SMOTE (Synthetic Minority Over-sampling Technique)
- Ajuste de threshold ótimo
- Class weights balanceados

### 3. **Feature Engineering Avançado**
- **Features numéricas derivadas**: IncomeToAge, YearsPerCompany, YearsWithoutPromotion, IncomeToEducation, DistanceSatisfactionRatio
- **Features binárias**: HighDistance, LowSatisfaction, NoPromotion, HighPerformer, YoungHighLevel
- **Scores compostos**: SatisfactionScore, WorkIntensity
- **Features categóricas**: AgeGroup, IncomeGroup
- **Features Polinomiais**: JobSatisfaction*MonthlyIncome, JobSatisfaction*StockOptionLevel, MonthlyIncome*SatisfactionScore, PercentSalaryHike*LowSatisfaction, PerformanceRating*LowSatisfaction, RelationshipSatisfaction*LowSatisfaction, LowSatisfaction^2, LowSatisfaction*WorkIntensity

### 4. **Visualizações e Relatórios**
- Curvas ROC e Precision-Recall
- Matrizes de confusão detalhadas
- Feature importance analysis
- Análise de threshold ótimo
- Relatórios automatizados em texto e JSON

## 📦 Estrutura do Projeto

## 🛠️ Tecnologias Utilizadas

### Bibliotecas Principais
- **pandas** & **numpy**: Manipulação de dados
- **scikit-learn**: Algoritmos de ML e pré-processamento
- **lightgbm**: Gradient Boosting com suporte a GPU
- **optuna**: Otimização bayesiana de hiperparâmetros
- **imbalanced-learn**: Técnicas de balanceamento (SMOTE)
- **matplotlib** & **seaborn**: Visualizações

## 🔧 Instalação

1. **Clone o repositório**
```bash
git clone https://github.com/matheuspavanids/project-ml-mackenzie.git
cd project-ml-mackenzie
```

2. **Crie um ambiente virtual**
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
# ou
venv\Scripts\activate  # Windows
```

3. **Instale as dependências**
```bash
pip install pandas numpy scikit-learn lightgbm optuna imbalanced-learn matplotlib seaborn joblib
```

## 💻 Como Usar

### Executar Pipeline Completo

```python
from main_pipeline import run_complete_pipeline


## 📊 Features Mais Importantes

### Top 9 Features (LightGBM)
1. **YearsAtCompany**: Anos na empresa atual
2. **NumCompaniesWorked**: Número de empresas em que já trabalhou
3. **WorkLifeBalance**: Equilíbrio entre vida pessoal e trabalho
4. **MonthlyIncome**: Renda Mensal
5. **DailyRate**: Remuneração fixa diária
6. **DistanceFromHome**: Distância de casa até o trabalho
7. **IncomeToEducation**: Renda em relação ao nível educacional
8. **MonthlyRate**: Remuneração fixa mensal
9. **PercentSalaryHike**: Aumento percentual no salário

## 📈 Métricas de Performance

| Modelo | Precision | Recall | F1-Score | AUC-ROC | Tempo (s) |
|--------|-----------|--------|----------|---------|-----------|
| RandomForest | 0.234 | 0.777 | 0.360 | 0.662 | 16729.58 |
| LogisticRegression | 0.184 | 0.986 | 0.311 | 0.657 | 2946.81 |
| **LightGBM** | **0.286** | **0.512** | **0.367** | **0.675** | 1874.88 |
| RidgeClassifier | 0.181 | 0.995 | 0.306 | 0.657 | 446.92 |
| VotingEnsemble | 0.256 | 0.668 | 0.370 | 0.671 | 0.0 |

## 🔍 Insights do Negócio

1. **Fatores Críticos de Attrition**:
   - Funcionários com mais tempode de casa e mais empresas trabalhadas se mostraram features relevantes para o modelo
   - Distância do trabalho se mostrou um fator relavante para saída de funcionário
   - Desequilíbrio vida-trabalho aumenta risco de saída

3. **Recomendações para RH**:
   - Incentivar contratação de funcionários que morem próximo a empresa
   - Programas de well-being para melhorar work-life balance
   - Incentivo a quem tem mais tempo de casa

## 👥 Autor

**Guilherme Camargo**
- GitHub: [@matheuspavanids](https://github.com/matheuspavanids)
- Projeto desenvolvido para Universidade Presbiteriana Mackenzie

**Projeto desenvolvimento para disciplina de Data Science ministrada pelo professor Matheus Pavani**