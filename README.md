# Predição do Valor de Imóveis em São Paulo

Projeto de regressão para prever o **preço de venda** e o **preço de aluguel** de apartamentos na cidade de São Paulo.

## Integrantes

| Nome | Matrícula |
|---|---|
| Thalys Eduardo Ferreira Cazuza | 20241180148 |
| Arthur Rodrigues de Carvalho | 20241130037 |
| Ramon Porfírio Macedo | 20241130023 |

## TDE 04: Modelo final

| Arquivo | O que é |
|---|---|
| `TDE04_Modelo_Final_Imoveis_SP.ipynb` | Notebook com a implementação, a comparação dos modelos e a discussão dos resultados |
| `Slides_TDE04_Imoveis_SP.pptx` | Slides da apresentação (com roteiro nas anotações de cada slide) |
| `Slides_TDE04_Imoveis_SP.pdf` | Os mesmos slides em PDF (para enviar no AVA) |
| `resultados_tde04.csv` | Métricas de todos os modelos (gerado pelo notebook) |
| `sao-paulo-properties-april-2019.csv` | Base de dados |

### O que mudou em relação ao baseline (TDE 03)

1. **Distrito como variável** (one-hot encoding): de 12 para 108 variáveis;
2. **Normalização** das variáveis e do preço (`StandardScaler`);
3. **Hiperparâmetros escolhidos com validação cruzada** (`GridSearchCV`, 5 partes), sem olhar o teste;
4. **Modelos novos:** Ridge (Polinomial + regularização), **SVM (SVR)**, **Rede Neural (MLP)** e **Random Forest**
   (vistos em sala), mais dois modelos **não vistos em sala**: **Gradient Boosting** (em sala o boosting foi visto só
   com o AdaBoost) e **KNN**.

A divisão treino/teste é a mesma do TDE 03 (80/20, `random_state=42`), então todos os modelos são comparados nos mesmos imóveis.

### Resultados (dados de teste)

| Modelo | Etapa | Venda: MAE | Venda: R² | Aluguel: MAE | Aluguel: R² |
|---|---|---|---|---|---|
| Chute da média | referência | R$ 397.450 | 0,00 | R$ 1.989 | 0,00 |
| Regressão Linear | TDE 03 | R$ 176.168 | 0,75 | R$ 1.137 | 0,63 |
| Regressão Polinomial (grau 2) | TDE 03 | R$ 154.654 | 0,69 | R$ 1.074 | 0,66 |
| Ridge (Polinomial + regularização) | TDE 04 | R$ 127.500 | 0,76 | R$ 841 | 0,67 |
| SVM (SVR) | TDE 04 | R$ 108.743 | 0,84 | R$ 719 | 0,76 |
| Rede Neural (MLP) | TDE 04 | R$ 110.473 | 0,85 | R$ 768 | 0,78 |
| Random Forest | TDE 04 | R$ 94.600 | 0,90 | **R$ 727** | 0,72 |
| Gradient Boosting | TDE 04 | **R$ 93.322** | 0,90 | R$ 713 | 0,74 |
| KNN | TDE 04 | R$ 127.489 | 0,82 | R$ 770 | 0,71 |

Em negrito: o modelo final de cada tipo, escolhido pelo menor MAE na **validação cruzada** (não pelo teste).
No aluguel, Random Forest (R$ 735) e Gradient Boosting (R$ 741) praticamente empataram na validação.

**Modelo final** (escolhido pelo menor MAE na validação cruzada):

- **Venda (Gradient Boosting):** MAE de R$ 93.322 (40% menor que o melhor baseline) e R² de 0,90;
- **Aluguel (Random Forest):** MAE de R$ 727 (32% menor que o melhor baseline) e R² de 0,72.

As metas definidas no TDE 03 (superar o melhor baseline em MAE e em R²) foram atingidas nos dois casos.

## TDE 03: Baseline

Regressão Linear e Regressão Polinomial (grau 2), sem otimizações. Está na branch `TDE3`
(notebook `TDE03_Baseline_Imoveis_SP.ipynb`) e é reproduzido na seção 7 do notebook do TDE 04.

## Dataset

- Fonte: [São Paulo Real Estate - Sale / Rent - April 2019 (Kaggle)](https://www.kaggle.com/datasets/argonalyst/sao-paulo-real-estate-sale-rent-april-2019)
- Arquivo: `sao-paulo-properties-april-2019.csv` (incluído no repositório)

## Como executar

1. Instale as bibliotecas: `pip install pandas numpy matplotlib scikit-learn jupyter`
2. Deixe o CSV na mesma pasta do notebook.
3. Abra o notebook e execute todas as células. Leva cerca de 4 minutos em um computador com 12 núcleos lógicos
   (a busca de hiperparâmetros é a parte mais demorada); no Google Colab gratuito deve demorar bem mais.

No Google Colab, faça o upload do CSV antes de executar.

Com versões diferentes das bibliotecas (por exemplo, no Colab), os números podem mudar um pouco, principalmente o da
Regressão Polinomial do baseline. Testamos também com pandas 2.2 e scikit-learn 1.6, e os modelos finais escolhidos foram os mesmos.
