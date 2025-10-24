# Projeto de Previsão da Resistência do Concreto

## 📝 Resumo do Projeto

Este projeto consiste em uma Análise Exploratória de Dados (EDA) e Modelagem Preditiva para determinar os fatores mais influentes na resistência à compressão do concreto. Utilizamos diversas técnicas de Regressão, incluindo a otimização de hiperparâmetros (Hyperparameter Tuning), para construir um modelo robusto capaz de prever a resistência do concreto com base na composição de seus materiais e idade de cura.

**Resultado Principal:** O modelo **Gradient Boosting Regressor (GBR)** otimizado alcançou um alto desempenho, com um **R² de 0.8117**, e identificou a **Idade de Cura (Age)** e a quantidade de **Cimento (Cement)** como os fatores mais críticos para a resistência final.

## ⚙️ Tecnologias e Bibliotecas

* **Python**
* **Pandas:** Manipulação e limpeza de dados.
* **Matplotlib / Seaborn:** Análise e visualização de dados.
* **Scikit-learn:** Modelagem (Regressão Linear, Random Forest, GBR) e técnicas de otimização (`RandomizedSearchCV`).

## 💾 Dados

O projeto utiliza o arquivo `dados_concreto_-_Sheet1.csv`. As colunas representam a composição dos materiais por metro cúbico (kg/m³) e a idade de cura (dias).

| Coluna | Descrição |
| :--- | :--- |
| `Cement` | Cimento (kg/m³) |
| `Blast Furnace Slag` | Escória de Alto Forno (kg/m³) |
| `Fly Ash` | Cinza Volante (kg/m³) |
| `Water` | Água (kg/m³) |
| `Superplasticizer` | Superplastificante (kg/m³) |
| `Coarse Aggregate` | Agregado Graúdo (kg/m³) |
| `Fine Aggregate` | Agregado Miúdo (kg/m³) |
| `Age` | Idade de cura (dias) |
| `Concrete compressive strength` | **TARGET:** Resistência à Compressão (MPa) |
| `Strength Category` | Categoria de Força (Alto/Baixa) |

## 🚀 Etapas da Análise

### 1. Pré-processamento e Limpeza

* **Tratamento de Nulos:** As 9 linhas com valores faltantes na variável alvo (`Concrete compressive strength`) foram removidas, por representarem menos de 0.5% do dataset.
* **Codificação Categórica:** A variável `Strength Category` foi convertida em binária (Label Encoding).

### 2. Análise Exploratória (EDA)

* **Correlação:** A correlação entre as variáveis e a resistência do concreto foi analisada, destacando:
    * **Correlação Positiva Moderada:** `Age`, `Cement` e `Superplasticizer`.
    * **Correlação Negativa/Nula:** `Water` e Agregados.
* **Visualização:** Gráficos de dispersão (`Cement` vs. `Strength`) e gráficos de barras (`Mean Strength by Category`) foram gerados para entender as tendências.

### 3. Modelagem de Regressão e Comparação

Três modelos foram testados para prever a `Concrete compressive strength`:

| Modelo | $R^2$ (Inicial) | MAE (Inicial) | Observação |
| :--- | :--- | :--- | :--- |
| **Regressão Linear** | $0.2049$ | $11.95 \text{ MPa}$ | Desempenho muito baixo, indicando relação não linear. |
| **Random Forest Regressor** | $0.2656$ | $11.30 \text{ MPa}$ | Melhor que o modelo linear, confirmando a não-linearidade. |
| **Gradient Boosting Regressor (GBR)** | $0.3211$ | $11.13 \text{ MPa}$ | Melhor modelo inicial. |

### 4. Otimização de Hiperparâmetros (Tuning)

O modelo **GBR** foi otimizado usando `RandomizedSearchCV` com uma validação cruzada (`cv=5`) para maximizar o $R^2$.

| Métrica | GBR (Inicial) | GBR (Otimizado) |
| :--- | :--- | :--- |
| **$R^2$** | $0.3211$ | **$0.8117$** |
| **MAE** | $11.13 \text{ MPa}$ | **$4.88 \text{ MPa}$** |

**Melhores Parâmetros Encontrados:**
```python
{'n_estimators': 200, 'min_samples_split': 5, 'max_features': 'log2', 'max_depth': 7, 'learning_rate': 0.1}
