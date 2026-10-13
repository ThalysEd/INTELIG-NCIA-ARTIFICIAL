# Predição do Valor de Imóveis em São Paulo

Projeto de regressão para prever o **preço de venda** e o **preço de aluguel** de imóveis na cidade de São Paulo.

## Integrantes

| Nome | Matrícula |
|---|---|
| Thalys Eduardo Ferreira Cazuza | 20241180148 |
| Arthur Rodrigues de Carvalho | 20241130037 |
| Ramon Porfírio Macedo | 20241130023 |

## TDE 03: Baseline

Notebook: `TDE03_Baseline_Imoveis_SP.ipynb`

Dois algoritmos vistos em sala, sem otimizações:

1. Regressão Linear
2. Regressão Polinomial (grau 2)

Métricas de avaliação: MAE, MSE, RMSE e R².

| | Modelo | MAE | R² |
|---|---|---|---|
| Venda | Regressão Linear | R$ 176.168 | 0,75 |
| Venda | Regressão Polinomial | R$ 154.654 | 0,69 |
| Aluguel | Regressão Linear | R$ 1.137 | 0,63 |
| Aluguel | Regressão Polinomial | R$ 1.074 | 0,66 |

## Dataset

- Fonte: [São Paulo Real Estate - Sale / Rent - April 2019 (Kaggle)](https://www.kaggle.com/datasets/argonalyst/sao-paulo-real-estate-sale-rent-april-2019)
- Arquivo: `sao-paulo-properties-april-2019.csv` (incluído no repositório)

## Como executar

1. Instale as bibliotecas: `pip install pandas numpy matplotlib scikit-learn jupyter`
2. Deixe o CSV na mesma pasta do notebook.
3. Abra o notebook e execute todas as células.

No Google Colab, faça o upload do CSV antes de executar.
