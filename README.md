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

- **F1-Score**: 0.378 (LightGBM)
- **Recall**: 0.624 (capacidade de identificar funcionários em risco)
- **AUC-ROC**: 0.672
- **Dataset**: 50.000 registros sintéticos baseados no padrão IBM HR Analytics

## 🚀 Funcionalidades

### 1. **Pipeline Completo de ML**
- Preparação automática de dados
- Feature engineering avançado (36 features originais → 66 features)
- Múltiplos modelos: Random Forest, Logistic Regression, LightGBM
- Otimização automática de hiperparâmetros com Optuna

### 2. **Tratamento de Desbalanceamento**
- SMOTE (Synthetic Minority Over-sampling Technique)
- Random Undersampling
- Estratégia combinada (SMOTE + Undersampling)
- Ajuste de threshold ótimo
- Class weights balanceados

### 3. **Feature Engineering Avançado**
- **Ratios financeiros**: IncomeToAge, YearsPerCompany, PromotionRate
- **Indicadores de risco**: CriticalDistance, CriticalSatisfaction, StuckInRole
- **Scores compostos**: OverallSatisfaction, WorkIntensity, RiskScore
- **Categorias derivadas**: ExperienceLevel, AgeGroup, IncomeLevel

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

### Requisitos do Sistema
- Python 3.8+
- GPU NVIDIA (opcional, para acelerar LightGBM)
- 8GB RAM mínimo (16GB recomendado)

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

# Executar com 50.000 amostras e estratégia SMOTE
pipeline = run_complete_pipeline(n_samples=50000, balance_strategy='smote')
```

### Fazer Predições em Novos Dados

```python
from main_pipeline import load_and_use_saved_model

# Carregar modelo salvo e fazer predições
load_and_use_saved_model()
```

### Comparar Estratégias de Balanceamento

```python
from main_pipeline import compare_strategies

# Comparar diferentes abordagens
compare_strategies()
```

### Usar a Classe Pipeline Diretamente

```python
from hr_attrition_pipeline import HRAttritionPipeline
import pandas as pd

# Criar instância
pipeline = HRAttritionPipeline(use_gpu=True, balance_strategy='smote')

# Carregar seus dados
df = pd.read_csv('seus_dados.csv')

# Preparar dados
X, y = pipeline.load_and_prepare_data(df)

# Feature engineering
X_engineered = pipeline.create_features(X)

# Split treino/teste
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(
    X_engineered, y, test_size=0.2, random_state=42, stratify=y
)

# Treinar modelos
pipeline.train_models(X_train, y_train, X_test, y_test)

# Gerar visualizações
pipeline.plot_results(X_test, y_test)

# Salvar melhor modelo
pipeline.save_best_model()
```

## 📊 Features Mais Importantes

### Top 10 Features (LightGBM)
1. **OverTime_Yes**: Trabalho em horas extras
2. **JobSatisfaction**: Satisfação com o trabalho
3. **WorkLifeBalance**: Equilíbrio vida-trabalho
4. **EnvironmentSatisfaction**: Satisfação com ambiente
5. **NumCompaniesWorked**: Número de empresas anteriores
6. **YearsAtCompany**: Anos na empresa atual
7. **YearsSinceLastPromotion**: Anos desde última promoção
8. **StockOptionLevel**: Nível de stock options
9. **JobLevel**: Nível hierárquico
10. **MaritalStatus_Married**: Estado civil casado

## 📈 Métricas de Performance

| Modelo | Precision | Recall | F1-Score | AUC-ROC | Tempo (s) |
|--------|-----------|--------|----------|---------|-----------|
| RandomForest | 0.267 | 0.574 | 0.364 | 0.659 | 429.2 |
| LogisticRegression | 0.248 | 0.629 | 0.356 | 0.645 | 108.8 |
| **LightGBM** | **0.271** | **0.624** | **0.378** | **0.673** | 3472.8 |

## 🔍 Insights do Negócio

1. **Fatores Críticos de Attrition**:
   - Funcionários com overtime têm 2x mais chance de sair
   - Baixa satisfação no trabalho é o 2º fator mais importante
   - Desequilíbrio vida-trabalho aumenta risco em 40%

2. **Perfis de Alto Risco**:
   - Jovens profissionais (< 25 anos) em vendas
   - Funcionários com 5+ anos sem promoção
   - Alta rotatividade prévia (4+ empresas)

3. **Recomendações para RH**:
   - Monitorar closely funcionários com overtime frequente
   - Programas de well-being para melhorar work-life balance
   - Revisão de política de promoções (máximo 3-4 anos)

## 🤝 Contribuindo

Contribuições são bem-vindas! Por favor:

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📝 Licença

Este projeto está licenciado sob a MIT License - veja o arquivo [LICENSE](LICENSE) para detalhes.

## 👥 Autor

**Matheus Pavan**
- GitHub: [@matheuspavanids](https://github.com/matheuspavanids)
- Projeto desenvolvido para Universidade Presbiteriana Mackenzie

## 🙏 Agradecimentos

- Universidade Presbiteriana Mackenzie
- Dataset inspirado no IBM HR Analytics Employee Attrition & Performance
- Comunidade open-source pelas excelentes bibliotecas

---

⭐ Se este projeto foi útil, considere dar uma estrela no GitHub!