# Análise de Modelos Lineares Mistos em Python

Este repositório contém a análise estatística do arquivo `(Jul_25) Dados demandas físicas FCWC 2025.xlsx`, utilizada para investigar fatores preditores das demandas físicas de jogadores na Copa do Mundo de Clubes (FCWC).

## Objetivo

- Analisar, por meio de modelos lineares mistos, o efeito de variáveis ambientais, demográficas e de jogo sobre a demanda física dos jogadores.
- Todas as etapas do script original foram escritas em R, incluindo tratamento de dados, análise descritiva, modelagem, diagnóstico e visualização.

## Estrutura do repositório

```
.
├── data/                # Dados brutos 
├── model/               # Notebooks e scripts de análise
    └── Modelo Linear Misto.Rmd
│   └── modelo-linear-misto-python.ipynb
├── .gitignore
├── README.md
└── requirements.txt     # Dependências do projeto
```

## Como rodar o projeto

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/SEU_USUARIO/linear-mixed-effects-model-fcwf-2025.git
   cd linear-mixed-effects-model-fcwf-2025
   ```

2. **Crie um ambiente virtual (recomendado):**
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

3. **Instale as dependências:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Abra o notebook:**
   ```bash
   code .
   # ou
   jupyter notebook model/modelo-linear-misto-python.ipynb
   ```

6. **Execute as células do notebook na ordem.**

## Observações importantes

- O notebook está comentado para facilitar o entendimento e adaptação.
- Caso utilize outro arquivo de dados, ajuste o caminho na célula de carregamento.

## Principais bibliotecas utilizadas

- pandas, numpy, matplotlib, seaborn
- statsmodels (modelos lineares mistos)
- pingouin (estatísticas descritivas)
- tabulate (tabelas)
- openpyxl (leitura de Excel)
- scikit-learn (centralização)
- scipy (testes estatísticos)

# Supplementary material

## Linearity check
**Fig S1: PairPlot between continuous predictors and high intensity distance covered per minute (Zones 4 and 5)**

<img src="images/FigS1-High-intensity-PairPlot.png" width="800" alt="Fig S1">

**Supplementary Figure 1:** Visual representation of the relationships between each continuous predictor and the outcome variable, high-intensity distance covered per minute (Zones 4 and 5). The lower half displays scatterplots, the upper half shows correlation coefficients, and the diagonal shows frequency distributions via histograms. WBGT: wet bulb globe temperature; Temp: dry air temperature; UR: relative humidity; Rad: radiation; TG: globe temperatue; TN: wet bulb temperatuer; UA: absolute humidity.

**Fig S2: PairPlot between continuous predictors and moderate intensity distance covered per minute (Zone 3)**

<img src="images/FigS2-Moderate-intensity-PairPlot.png" width="800" alt="Fig S2">

**Supplementary Figure 2:** Visual representation of the relationships between each continuous predictor and the outcome variable, moderate-intensity distance covered per minute (Zone 3). The lower half displays scatterplots, the upper half shows correlation coefficients, and the diagonal shows frequency distributions via histograms. WBGT: wet bulb globe temperature; Temp: dry air temperature; UR: relative humidity; Rad: radiation; TG: globe temperatue; TN: wet bulb temperatuer; UA: absolute humidity.


**Fig S3: PairPlot between continuous predictors and low intensity distance covered per minute (Zones 1 and 2).**

<img src="images/FigS3-Low-intensity-PairPlot.png" width="800" alt="Fig S3">

**Supplementary Figure 3:** Visual representation of the relationships between each continuous predictor and the outcome variable, low-intensity distance covered per minute (Zones 1 and 2). The lower half displays scatterplots, the upper half shows correlation coefficients, and the diagonal shows frequency distributions via histograms. WBGT: wet bulb globe temperature; Temp: dry air temperature; UR: relative humidity; Rad: radiation; TG: globe temperatue; TN: wet bulb temperatuer; UA: absolute humidity.


**Fig S4: PairPlot between continuous predictors and total distance covered per minute**

<img src="images/FigS4-Total-distance-PairPlot.png" width="800" alt="Fig S4">

**Supplementary Figure 4:** Visual representation of the relationships between each continuous predictor and the outcome variable, total distance covered per minute. The lower half displays scatterplots, the upper half shows correlation coefficients, and the diagonal shows frequency distributions via histograms. WBGT: wet bulb globe temperature; Temp: dry air temperature; UR: relative humidity; Rad: radiation; TG: globe temperatue; TN: wet bulb temperatuer; UA: absolute humidity.


## MODEL 1 - Assumption checks
VD ~ Stage + Time_of_day + Ranking_difference + Player_position + Player_age_c + Origin_climate + WBGT_c + (1 | Player_id) + Time_of_day * WBGT_c

### High intensity distance covered per minute (Zones 4 and 5)
**Table S1. Multicollinearity diagnosis**
|Predictor | VIF | VIF 95% CI | Increased SE | Tolerance | Tolerance 95% CI|
|:-----:|:-----:|:-------:|:--------------:|:-----------:|:-----------------:|
| Stage | 1.23 | [1.16, 1.34] | 1.11 | 0.81 | [0.75, 0.86] |
| Time_of_day | 1.22 | [1.15, 1.32] | 1.10 | 0.82 | [0.76, 0.87] |
| Ranking_difference | 1.15 | [1.09, 1.25] | 1.07 | 0.87 | [0.80, 0.92] |
| Player_position | 1.02 | [1.00, 1.42] | 1.01 | 0.98 | [0.71, 1.00] |
| Player_age_c | 1.04 | [1.01, 1.19] | 1.02 | 0.96 | [0.84, 0.99] |
| Origin_climate | 1.05 | [1.01, 1.18] | 1.02 | 0.95 | [0.84, 0.99] |
| WBGT_c | 1.69 | [1.56, 1.85] | 1.30 | 0.59 | [0.54, 0.64] |
| Time_of_day:WBGT_c | 1.59 | [1.47, 1.73] | 1.26 | 0.63 | [0.58, 0.68] |

**Supplementary Table 1:** Results of the multicollinearity diagnosis for model 1 and and the outcome variable high intensity distance covered per minute. Variance Inflation Factor (VIF), Increased Standard Error, and Tolerance values for each predictor in the model. These metrics assess the degree of multicollinearity among the continuous predictor variables. VIF > 10 indicates high multicollinearity and VIF > 5 indicates moderate multicollinearity.
 
**Fig S5: Histogram and Q-Q Plot of residuals; scatterplot residuals x fitted. Graphical analysis of normality and homoscedasticity of residuals**

<img src="images/FigS5-High-intensity-model1-residuals-check.png" width="800" alt="Fig S5">

**Supplementary Figure 5:** Graphical analysis of the model residuals for assumptions assessment. The histogram and Q-Q plot were used to visually assess the normality of the residuals. The scatterplot of residuals versus fitted values was used to assess the assumption of homoscedasticity.

**Fig S6: Histogram and Q-Q Plot of random effects**

<img src="images/FigS6-High-intensity-model1-random-effects-check.png" width="800" alt="Fig S6">

**Supplementary Figure 6**: Graphical assessment of the normality of the random effects. The histograms and Q-Q plots for each random effect are used to visually confirm the assumption that they are normally distributed.

**Table S2: Kolmogorov-Smirnov test for residuals and random effects normality check**
|Data| D | p-value|
|:--:|:--:|:-----:|
|Residuals|0.04|0.003*|
|Random effects|0.05|0.01*|

**Supplementary Table 2:** Kolmogorov-Smirnov test results to check the assumption of normality for both the model residuals and the random effects. The table shows the D statistic and the p-value for each test.

### Moderate intensity distance covered per minute (Zone 3)
**Table S3. Multicollinearity diagnosis**
|Predictor | VIF | VIF 95% CI | Increased SE | Tolerance | Tolerance 95% CI|
|:-----:|:-----:|:-------:|:--------------:|:-----------:|:-----------------:|
| Stage | 1.26 | [1.18, 1.36] | 1.12 | 0.80 | [0.73, 0.85] |
| Time_of_day | 1.22 | [1.15, 1.33] | 1.11 | 0.82 | [0.75, 0.87] |
| Ranking_difference | 1.18 | [1.11, 1.28] | 1.08 | 0.85 | [0.78, 0.90] |
| Player_position | 1.02 | [1.00, 1.47] | 1.01 | 0.98 | [0.68, 1.00] |
| Player_age_c | 1.04 | [1.01, 1.20] | 1.02 | 0.96 | [0.83, 0.99] |
| Origin_climate | 1.04 | [1.01, 1.19] | 1.02 | 0.96 | [0.84, 0.99] |
| WBGT_c | 1.68 | [1.56, 1.84] | 1.30 | 0.59 | [0.54, 0.64] |
| Time_of_day:WBGT_c | 1.57 | [1.46, 1.71] | 1.25 | 0.64 | [0.58, 0.69] |

**Supplementary Table 3:** Results of the multicollinearity diagnosis for model 1 and and the outcome variable moderate intensity distance covered per minute. Variance Inflation Factor (VIF), Increased Standard Error, and Tolerance values for each predictor in the model. These metrics assess the degree of multicollinearity among the continuous predictor variables. VIF > 10 indicates high multicollinearity and VIF > 5 indicates moderate multicollinearity.


**Fig S7: Histogram and Q-Q Plot of residuals; scatterplot residuals x fitted. Graphical analysis of normality and homoscedasticity of residuals**

<img src="images/FigS7-Moderate-intensity-model1-residuals-check.png" width="800" alt="Fig S7">

**Supplementary Figure 7:** Graphical analysis of the model residuals for assumptions assessment. The histogram and Q-Q plot were used to visually assess the normality of the residuals. The scatterplot of residuals versus fitted values was used to assess the assumption of homoscedasticity.

**Fig S8: Histogram and Q-Q Plot of random effects**

<img src="images/FigS8-Moderate-intensity-model1-random-effects-check.png" width="800" alt="Fig S8">

**Supplementary Figure 8**: Graphical assessment of the normality of the random effects. The histograms and Q-Q plots for each random effect are used to visually confirm the assumption that they are normally distributed.

**Table S4: Kolmogorov-Smirnov test for residuals and random effects normality check**
|Data| D | p-value|
|:--:|:--:|:-----:|
|Residuals|0.03|0.009*|
|Random effects|0.04|0.05|

**Supplementary Table 4:** Kolmogorov-Smirnov test results to check the assumption of normality for both the model residuals and the random effects. The table shows the D statistic and the p-value for each test.


### Low intensity distance covered per minute (Zones 1 and 2)
**Table S5. Multicollinearity diagnosis**
|Predictor | VIF | VIF 95% CI | Increased SE | Tolerance | Tolerance 95% CI|
|:-----:|:-----:|:-------:|:--------------:|:-----------:|:-----------------:|
| Stage | 1.24 | [1.17, 1.34] | 1.11 | 0.81 | [0.74, 0.86] |
| Time_of_day | 1.22 | [1.15, 1.32] | 1.10 | 0.82 | [0.76, 0.87] |
| Ranking_difference | 1.16 | [1.10, 1.26] | 1.08 | 0.86 | [0.80, 0.91] |
| Player_position | 1.02 | [1.00, 1.43] | 1.01 | 0.98 | [0.70, 1.00] |
| Player_age_c | 1.04 | [1.01, 1.19] | 1.02 | 0.96 | [0.84, 0.99] |
| Origin_climate | 1.05 | [1.01, 1.19] | 1.02 | 0.95 | [0.84, 0.99] |
| WBGT_c | 1.69 | [1.56, 1.85] | 1.30 | 0.59 | [0.54, 0.64] |
| Time_of_day:WBGT_c | 1.58 | [1.47, 1.73] | 1.26 | 0.63 | [0.58, 0.68] |

**Supplementary Table 5:** Results of the multicollinearity diagnosis for model 1 and and the outcome variable low intensity distance covered per minute. Variance Inflation Factor (VIF), Increased Standard Error, and Tolerance values for each predictor in the model. These metrics assess the degree of multicollinearity among the continuous predictor variables. VIF > 10 indicates high multicollinearity and VIF > 5 indicates moderate multicollinearity.


**Fig S9: Histogram and Q-Q Plot of residuals; scatterplot residuals x fitted. Graphical analysis of normality and homoscedasticity of residuals**

<img src="images/FigS9-Low-intensity-model1-residuals-check.png" width="800" alt="Fig S9">

**Supplementary Figure 9:** Graphical analysis of the model residuals for assumptions assessment. The histogram and Q-Q plot were used to visually assess the normality of the residuals. The scatterplot of residuals versus fitted values was used to assess the assumption of homoscedasticity.


**Fig S10: Histogram and Q-Q Plot of random effects**

<img src="images/FigS10-Low-intensity-model1-random-effects-check.png" width="800" alt="Fig S10">

**Supplementary Figure 10**: Graphical assessment of the normality of the random effects. The histograms and Q-Q plots for each random effect are used to visually confirm the assumption that they are normally distributed.

**Table S6: Kolmogorov-Smirnov test for residuals and random effects normality check**
|Data| D | p-value|
|:--:|:--:|:-----:|
|Residuals|0.02|0.4|
|Random effects|0.03|0.5|

**Supplementary Table 6:** Kolmogorov-Smirnov test results to check the assumption of normality for both the model residuals and the random effects. The table shows the D statistic and the p-value for each test.


### Total distance covered per minute
**Table S7. Multicollinearity diagnosis**
|Predictor | VIF | VIF 95% CI | Increased SE | Tolerance | Tolerance 95% CI|
|:-----:|:-----:|:-------:|:--------------:|:-----------:|:-----------------:|
|Stage|1.26 |[1.18, 1.37]|    1.12      |    0.79   |  [0.73, 0.85]   |
|Time_of_day| 1.22 |[1.15, 1.33]  |       1.11  |    0.82   |  [0.75, 0.87]|
|Ranking_difference| 1.18| [1.12, 1.28]|         1.09|      0.85|     [0.78, 0.90]|
|Player_position |1.02| [1.00, 1.47]|         1.01|      0.98|     [0.68, 1.00]|
|Player_age_c | 1.04 | [1.01, 1.20] |        1.02|      0.96 |    [0.83, 0.99]|
|Origin_climate |1.04| [1.01, 1.19] |        1.02|      0.96 |     [0.84, 0.99]|
|WBGT_c |1.68 | [1.55, 1.84]|         1.30 |     0.59 |    [0.54, 0.64]|
|Time_of_day:WBGT_c | 1.57 | [1.46, 1.71] |        1.25|      0.64|     [0.58, 0.69]|

**Supplementary Table 7:** Results of the multicollinearity diagnosis for model 1 and and the outcome variable total distance covered per minute. Variance Inflation Factor (VIF), Increased Standard Error, and Tolerance values for each predictor in the model. These metrics assess the degree of multicollinearity among the continuous predictor variables. VIF > 10 indicates high multicollinearity and VIF > 5 indicates moderate multicollinearity.

**Fig S11: Histogram and Q-Q Plot of residuals; scatterplot residuals x fitted. Graphical analysis of normality and homoscedasticity of residuals**

<img src="images/FigS11-Total-distance-model1-residuals-check.png" width="800" alt="Fig S11">

**Supplementary Figure 11:** Graphical analysis of the model residuals for assumptions assessment. The histogram and Q-Q plot were used to visually assess the normality of the residuals. The scatterplot of residuals versus fitted values was used to assess the assumption of homoscedasticity.

**Fig S12: Histogram and Q-Q Plot of random effects**

<img src="images/FigS12-Total-distance-model1-random-effects-check.png" width="800" alt="Fig S12">

**Supplementary Figure 12**: Graphical assessment of the normality of the random effects. The histograms and Q-Q plots for each random effect are used to visually confirm the assumption that they are normally distributed.

**Table S8: Kolmogorov-Smirnov test for residuals and random effects normality check**
|Data| D | p-value|
|:--:|:--:|:-----:|
|Residuals|0.03|0.04*|
|Random effects|0.02|0.9|

**Supplementary Table 8:** Kolmogorov-Smirnov test results to check the assumption of normality for both the model residuals and the random effects. The table shows the D statistic and the p-value for each test.


## MODEL 2 - Assumption checks
VD ~ Stage + Time_of_day + Ranking_difference + Player_position + Player_age_c + Origin_climate + Temp_c + UR_c + RAD_c + (1 | Player_id) + Time_of_day * Temp_c + Time_of_day * UR_c

### High intensity distance covered per minute (Zones 4 and 5)
**Table S9. Multicollinearity diagnosis**
|Predictor | VIF | VIF 95% CI | Increased SE | Tolerance | Tolerance 95% CI|
|:-----:|:-----:|:-------:|:--------------:|:-----------:|:-----------------:|
| Stage | 1.51 | [1.40, 1.65] | 1.23 | 0.66 | [0.61, 0.71] |
| Time_of_day | 4.51 | [4.06, 5.01] | 2.12 | 0.22 | [0.20, 0.25] |
| Ranking_difference | 1.16 | [1.10, 1.26] | 1.08 | 0.86 | [0.80, 0.91] |
| Player_position | 1.02 | [1.00, 1.39] | 1.01 | 0.98 | [0.72, 1.00] |
| Player_age_c | 1.04 | [1.01, 1.19] | 1.02 | 0.96 | [0.84, 0.99] |
| Origin_climate | 1.05 | [1.02, 1.18] | 1.03 | 0.95 | [0.85, 0.98] |
| Temp_c | 3.04 | [2.76, 3.36] | 1.74 | 0.33 | [0.30, 0.36] |
| UR_c | 4.13 | [3.73, 4.59] | 2.03 | 0.24 | [0.22, 0.27] |
| Time_of_day:Temp_c | 1.92 | [1.76, 2.10] | 1.38 | 0.52 | [0.48, 0.57] |
| Time_of_day:UR_c | 2.15 | [1.97, 2.37] | 1.47 | 0.46 | [0.42, 0.51] |
| RAD_c | 5.44 | [4.89, 6.06] | 2.33 | 0.18 | [0.16, 0.20] |

**Supplementary Table 9:** Results of the multicollinearity diagnosis for model 2 and and the outcome variable high intensity distance covered per minute. Variance Inflation Factor (VIF), Increased Standard Error, and Tolerance values for each predictor in the model. These metrics assess the degree of multicollinearity among the continuous predictor variables. VIF > 10 indicates high multicollinearity and VIF > 5 indicates moderate multicollinearity.

**Fig S13: Histogram and Q-Q Plot of residuals; scatterplot residuals x fitted. Graphical analysis of normality and homoscedasticity of residuals**

<img src="images/FigS13-High-intensity-model2-residuals-check.png" width="800" alt="Fig S13">

**Supplementary Figure 13:** Graphical analysis of the model residuals for assumptions assessment. The histogram and Q-Q plot were used to visually assess the normality of the residuals. The scatterplot of residuals versus fitted values was used to assess the assumption of homoscedasticity.

**Fig S14: Histogram and Q-Q Plot of random effects**

<img src="images/FigS14-High-intensity-model2-random-effects-check.png" width="800" alt="Fig S14">

**Supplementary Figure 14**: Graphical assessment of the normality of the random effects. The histograms and Q-Q plots for each random effect are used to visually confirm the assumption that they are normally distributed.

**Table S10: Kolmogorov-Smirnov test for residuals and random effects normality check**
|Data| D | p-value|
|:--:|:--:|:-----:|
|Residuals|0.04|0.001*|
|Random effects|0.05|0.004*|

**Supplementary Table 10:** Kolmogorov-Smirnov test results to check the assumption of normality for both the model residuals and the random effects. The table shows the D statistic and the p-value for each test.

### Moderate intensity distance covered per minute (Zone 3)
**Table S11. Multicollinearity diagnosis**
|Predictor | VIF | VIF 95% CI | Increased SE | Tolerance | Tolerance 95% CI|
|:-----:|:-----:|:-------:|:--------------:|:-----------:|:-----------------:|
| Stage | 1.55 | [1.44, 1.69] | 1.25 | 0.64 | [0.59, 0.69] |
| Time_of_day | 4.50 | [4.05, 5.00] | 2.12 | 0.22 | [0.20, 0.25] |
| Ranking_difference | 1.19 | [1.12, 1.29] | 1.09 | 0.84 | [0.78, 0.89] |
| Player_position | 1.02 | [1.00, 1.44] | 1.01 | 0.98 | [0.70, 1.00] |
| Player_age_c | 1.04 | [1.01, 1.20] | 1.02 | 0.96 | [0.84, 0.99] |
| Origin_climate | 1.05 | [1.01, 1.18] | 1.02 | 0.95 | [0.84, 0.99] |
| Temp_c | 3.16 | [2.87, 3.50] | 1.78 | 0.32 | [0.29, 0.35] |
| UR_c | 4.19 | [3.78, 4.65] | 2.05 | 0.24 | [0.21, 0.26] |
| Time_of_day:Temp_c | 1.92 | [1.76, 2.10] | 1.38 | 0.52 | [0.48, 0.57] |
| Time_of_day:UR_c | 2.14 | [1.97, 2.36] | 1.46 | 0.47 | [0.42, 0.51] |
| RAD_c | 5.44 | [4.89, 6.06] | 2.33 | 0.18 | [0.17, 0.20] |

**Supplementary Table 11:** Results of the multicollinearity diagnosis for model 2 and and the outcome variable moderate intensity distance covered per minute. Variance Inflation Factor (VIF), Increased Standard Error, and Tolerance values for each predictor in the model. These metrics assess the degree of multicollinearity among the continuous predictor variables. VIF > 10 indicates high multicollinearity and VIF > 5 indicates moderate multicollinearity.

**Fig S15: Histogram and Q-Q Plot of residuals; scatterplot residuals x fitted. Graphical analysis of normality and homoscedasticity of residuals**

<img src="images/FigS15-Moderate-intensity-model2-residuals-check.png" width="800" alt="Fig S15">

**Supplementary Figure 15:** Graphical analysis of the model residuals for assumptions assessment. The histogram and Q-Q plot were used to visually assess the normality of the residuals. The scatterplot of residuals versus fitted values was used to assess the assumption of homoscedasticity.

**Fig S16: Histogram and Q-Q Plot of random effects**

<img src="images/FigS16-Moderate-intensity-model2-random-effects-check.png" width="800" alt="Fig S16">

**Supplementary Figure 16**: Graphical assessment of the normality of the random effects. The histograms and Q-Q plots for each random effect are used to visually confirm the assumption that they are normally distributed.

**Table S12: Kolmogorov-Smirnov test for residuals and random effects normality check**
|Data| D | p-value|
|:--:|:--:|:-----:|
|Residuals|0.04|0.002*|
|Random effects|0.04|0.09|

**Supplementary Table 12:** Kolmogorov-Smirnov test results to check the assumption of normality for both the model residuals and the random effects. The table shows the D statistic and the p-value for each test.

### Low intensity distance covered per minute (Zones 1 and 2)
**Table S13. Multicollinearity diagnosis**
|Predictor | VIF | VIF 95% CI | Increased SE | Tolerance | Tolerance 95% CI|
|:-----:|:-----:|:-------:|:--------------:|:-----------:|:-----------------:|
| Stage | 1.52 | [1.41, 1.65] | 1.23 | 0.66 | [0.60, 0.71] |
| Time_of_day | 4.50 | [4.06, 5.01] | 2.12 | 0.22 | [0.20, 0.25] |
| Ranking_difference | 1.16 | [1.10, 1.26] | 1.08 | 0.86 | [0.79, 0.91] |
| Player_position | 1.02 | [1.00, 1.40] | 1.01 | 0.98 | [0.71, 1.00] |
| Player_age_c | 1.04 | [1.01, 1.19] | 1.02 | 0.96 | [0.84, 0.99] |
| Origin_climate | 1.05 | [1.02, 1.18] | 1.03 | 0.95 | [0.85, 0.99] |
| Temp_c | 3.06 | [2.78, 3.39] | 1.75 | 0.33 | [0.30, 0.36] |
| UR_c | 4.14 | [3.74, 4.60] | 2.04 | 0.24 | [0.22, 0.27] |
| Time_of_day:Temp_c | 1.92 | [1.76, 2.10] | 1.38 | 0.52 | [0.48, 0.57] |
| Time_of_day:UR_c | 2.15 | [1.97, 2.37] | 1.47 | 0.46 | [0.42, 0.51] |
| RAD_c | 5.44 | [4.89, 6.06] | 2.33 | 0.18 | [0.17, 0.20] |

**Supplementary Table 13:** Results of the multicollinearity diagnosis for model 2 and and the outcome variable low intensity distance covered per minute. Variance Inflation Factor (VIF), Increased Standard Error, and Tolerance values for each predictor in the model. These metrics assess the degree of multicollinearity among the continuous predictor variables. VIF > 10 indicates high multicollinearity and VIF > 5 indicates moderate multicollinearity.

**Fig S17: Histogram and Q-Q Plot of residuals; scatterplot residuals x fitted. Graphical analysis of normality and homoscedasticity of residuals**

<img src="images/FigS17-Low-intensity-model2-residuals-check.png" width="800" alt="Fig S17">

**Supplementary Figure 17:** Graphical analysis of the model residuals for assumptions assessment. The histogram and Q-Q plot were used to visually assess the normality of the residuals. The scatterplot of residuals versus fitted values was used to assess the assumption of homoscedasticity.

**Fig S18: Histogram and Q-Q Plot of random effects**

<img src="images/FigS18-Low-intensity-model2-random-effects-check.png" width="800" alt="Fig S18">

**Supplementary Figure 18**: Graphical assessment of the normality of the random effects. The histograms and Q-Q plots for each random effect are used to visually confirm the assumption that they are normally distributed.

**Table S14: Kolmogorov-Smirnov test for residuals and random effects normality check**
|Data| D | p-value|
|:--:|:--:|:-----:|
|Residuals|0.02|0.4|
|Random effects|0.03|0.3|

**Supplementary Table 14:** Kolmogorov-Smirnov test results to check the assumption of normality for both the model residuals and the random effects. The table shows the D statistic and the p-value for each test.


### Total distance covered per minute
**Table S15. Multicollinearity diagnosis**
|Predictor | VIF | VIF 95% CI | Increased SE | Tolerance | Tolerance 95% CI|
|:-----:|:-----:|:-------:|:--------------:|:-----------:|:-----------------:|
|Stage| 1.56 |[1.44, 1.70]|         1.25|      0.64|     [0.59, 0.69]|
|Time_of_day |4.49 |[4.05, 5.00] |        2.12|      0.22|     [0.20, 0.25]|
|Ranking_difference |1.19 |[1.12, 1.29]|         1.09|      0.84|     [0.77, 0.89]|
|Player_position | 1.02 |[1.00, 1.44] |         1.01|      0.98|     [0.69, 1.00]|
|Player_age_c | 1.04| [1.01, 1.20]|         1.02|      0.96|     [0.84, 0.99]|
|Origin_climate |1.05 |[1.01, 1.19]|         1.02|      0.95|     [0.84, 0.99]|
|Temp_c |3.17 |[2.87, 3.51] |        1.78|      0.32|     [0.29, 0.35]|
|UR_c |4.19 |[3.78, 4.66]|         2.05|      0.24|     [0.21, 0.26]|
|Time_of_day:Temp_c |1.92| [1.76, 2.10]|         1.38|      0.52|     [0.48, 0.57]|
|Time_of_day:UR_c |2.14 |[1.96, 2.35] |        1.46|      0.47|     [0.42, 0.51]|
|RAD_c |5.44 |[4.89, 6.06]|         2.33|      0.18|     [0.17, 0.20]|

**Supplementary Table 15:** Results of the multicollinearity diagnosis for model 2 and and the outcome variable total distance covered per minute. Variance Inflation Factor (VIF), Increased Standard Error, and Tolerance values for each predictor in the model. These metrics assess the degree of multicollinearity among the continuous predictor variables. VIF > 10 indicates high multicollinearity and VIF > 5 indicates moderate multicollinearity.

**Fig S19: Histogram and Q-Q Plot of residuals; scatterplot residuals x fitted. Graphical analysis of normality and homoscedasticity of residuals**

<img src="images/FigS19-Total-distance-model2-residuals-check.png" width="800" alt="Fig S19">

**Supplementary Figure 19:** Graphical analysis of the model residuals for assumptions assessment. The histogram and Q-Q plot were used to visually assess the normality of the residuals. The scatterplot of residuals versus fitted values was used to assess the assumption of homoscedasticity.

**Fig S20: Histogram and Q-Q Plot of random effects**

<img src="images/FigS20-Total-distance-model2-random-effects-check.png" width="800" alt="Fig S20">

**Supplementary Figure 20**: Graphical assessment of the normality of the random effects. The histograms and Q-Q plots for each random effect are used to visually confirm the assumption that they are normally distributed.

**Table S16: Kolmogorov-Smirnov test for residuals and random effects normality check**
|Data| D | p-value|
|:--:|:--:|:-----:|
|Residuals|0.03|0.06|
|Random effects|0.02|0.9|

**Supplementary Table 16:** Kolmogorov-Smirnov test results to check the assumption of normality for both the model residuals and the random effects. The table shows the D statistic and the p-value for each test.

## MODEL 5 - Assumption checks
VD ~ Stage + Time_of_day + Ranking_difference + Player_position + Player_age_c + Origin_climate + WBGT_c + UR_c + (1 | Player_id) + Time_of_day * UR_c + Time_of_day * WBGT_c

### High intensity distance covered per minute (Zones 4 and 5)
**Table S17. multicollinearity diagnosis**
|Predictor | VIF | VIF 95% CI | Increased SE | Tolerance | Tolerance 95% CI|
|:-----:|:-----:|:-------:|:--------------:|:-----------:|:-----------------:|
| Stage | 1.38 | [1.29, 1.50] | 1.18 | 0.72 | [0.66, 0.77] |
| Time_of_day | 1.36 | [1.27, 1.48] | 1.17 | 0.74 | [0.68, 0.79] |
| Ranking_difference | 1.15 | [1.09, 1.25] | 1.07 | 0.87 | [0.80, 0.92] |
| Player_position | 1.02 | [1.00, 1.40] | 1.01 | 0.98 | [0.71, 1.00] |
| Player_age_c | 1.04 | [1.01, 1.19] | 1.02 | 0.96 | [0.84, 0.99] |
| Origin_climate | 1.05 | [1.01, 1.18] | 1.03 | 0.95 | [0.85, 0.99] |
| WBGT_c | 2.06 | [1.89, 2.26] | 1.43 | 0.49 | [0.44, 0.53] |
| UR_c | 2.09 | [1.92, 2.30] | 1.45 | 0.48 | [0.44, 0.52] |
| Time_of_day:UR_c | 1.72 | [1.59, 1.88] | 1.31 | 0.58 | [0.53, 0.63] |
| Time_of_day:WBGT_c | 1.70 | [1.57, 1.86] | 1.30 | 0.59 | [0.54, 0.64] |

**Supplementary Table 17:** Results of the multicollinearity diagnosis for model 5 and and the outcome variable high intensity distance covered per minute. Variance Inflation Factor (VIF), Increased Standard Error, and Tolerance values for each predictor in the model. These metrics assess the degree of multicollinearity among the continuous predictor variables. VIF > 10 indicates high multicollinearity and VIF > 5 indicates moderate multicollinearity.

**Fig S21: Histogram and Q-Q Plot of residuals; scatterplot residuals x fitted. Graphical analysis of normality and homoscedasticity of residuals**

<img src="images/FigS21-High-intensity-model5-residuals-check.png" width="800" alt="Fig S21">

**Supplementary Figure 21:** Graphical analysis of the model residuals for assumptions assessment. The histogram and Q-Q plot were used to visually assess the normality of the residuals. The scatterplot of residuals versus fitted values was used to assess the assumption of homoscedasticity.

**Fig S22: Histogram and Q-Q Plot of random effects**

<img src="images/FigS22-High-intensity-model5-random-effects-check.png" width="800" alt="Fig S22">

**Supplementary Figure 22**: Graphical assessment of the normality of the random effects. The histograms and Q-Q plots for each random effect are used to visually confirm the assumption that they are normally distributed.

**Table S18: Kolmogorov-Smirnov test for residuals and random effects normality check**
|Data| D | p-value|
|:--:|:--:|:-----:|
|Residuals|0.04|0.0009*|
|Random effects|0.05|0.006*|

**Supplementary Table 18:** Kolmogorov-Smirnov test results to check the assumption of normality for both the model residuals and the random effects. The table shows the D statistic and the p-value for each test.

### Moderate intensity distance covered per minute (Zone 3)
**Table S19. multicollinearity diagnosis**
|Predictor | VIF | VIF 95% CI | Increased SE | Tolerance | Tolerance 95% CI|
|:-----:|:-----:|:-------:|:--------------:|:-----------:|:-----------------:|
| Stage | 1.42 | [1.33, 1.55] | 1.19 | 0.70 | [0.65, 0.75] |
| Time_of_day | 1.36 | [1.27, 1.48] | 1.17 | 0.74 | [0.68, 0.79] |
| Ranking_difference | 1.18 | [1.12, 1.28] | 1.09 | 0.85 | [0.78, 0.89] |
| Player_position | 1.02 | [1.00, 1.45] | 1.01 | 0.98 | [0.69, 1.00] |
| Player_age_c | 1.04 | [1.01, 1.20] | 1.02 | 0.96 | [0.84, 0.99] |
| Origin_climate | 1.05 | [1.01, 1.19] | 1.02 | 0.96 | [0.84, 0.99] |
| WBGT_c | 2.10 | [1.92, 2.30] | 1.45 | 0.48 | [0.43, 0.52] |
| UR_c | 2.11 | [1.94, 2.32] | 1.45 | 0.47 | [0.43, 0.52] |
| Time_of_day:UR_c | 1.70 | [1.57, 1.86] | 1.31 | 0.59 | [0.54, 0.64] |
| Time_of_day:WBGT_c | 1.69 | [1.56, 1.84] | 1.30 | 0.59 | [0.54, 0.64] |

**Supplementary Table 19:** Results of the multicollinearity diagnosis for model 5 and and the outcome variable moderate intensity distance covered per minute. Variance Inflation Factor (VIF), Increased Standard Error, and Tolerance values for each predictor in the model. These metrics assess the degree of multicollinearity among the continuous predictor variables. VIF > 10 indicates high multicollinearity and VIF > 5 indicates moderate multicollinearity.

**Fig S23: Histogram and Q-Q Plot of residuals; scatterplot residuals x fitted. Graphical analysis of normality and homoscedasticity of residuals**

<img src="images/FigS23-Moderate-intensity-model5-residuals-check.png" width="800" alt="Fig S23">

**Supplementary Figure 23:** Graphical analysis of the model residuals for assumptions assessment. The histogram and Q-Q plot were used to visually assess the normality of the residuals. The scatterplot of residuals versus fitted values was used to assess the assumption of homoscedasticity.

**Fig S24: Histogram and Q-Q Plot of random effects**

<img src="images/FigS24-Moderate-intensity-model5-random-effects-check.png" width="800" alt="Fig S24">

**Supplementary Figure 24**: Graphical assessment of the normality of the random effects. The histograms and Q-Q plots for each random effect are used to visually confirm the assumption that they are normally distributed.

**Table S20: Kolmogorov-Smirnov test for residuals and random effects normality check**
|Data| D | p-value|
|:--:|:--:|:-----:|
|Residuals|0.03|0.008*|
|Random effects|0.04|0.06|

**Supplementary Table 20:** Kolmogorov-Smirnov test results to check the assumption of normality for both the model residuals and the random effects. The table shows the D statistic and the p-value for each test.

### Low intensity distance covered per minute (Zones 1 and 2)
**Table S21. multicollinearity diagnosis**
|Predictor | VIF | VIF 95% CI | Increased SE | Tolerance | Tolerance 95% CI|
|:-----:|:-----:|:-------:|:--------------:|:-----------:|:-----------------:|
| Stage | 1.39 | [1.30, 1.51] | 1.18 | 0.72 | [0.66, 0.77] |
| Time_of_day | 1.36 | [1.27, 1.48] | 1.17 | 0.74 | [0.68, 0.79] |
| Ranking_difference | 1.16 | [1.10, 1.26] | 1.08 | 0.86 | [0.79, 0.91] |
| Player_position | 1.02 | [1.00, 1.41] | 1.01 | 0.98 | [0.71, 1.00] |
| Player_age_c | 1.04 | [1.01, 1.19] | 1.02 | 0.96 | [0.84, 0.99] |
| Origin_climate | 1.05 | [1.01, 1.18] | 1.02 | 0.95 | [0.85, 0.99] |
| WBGT_c | 2.07 | [1.90, 2.27] | 1.44 | 0.48 | [0.44, 0.53] |
| UR_c | 2.10 | [1.92, 2.30] | 1.45 | 0.48 | [0.43, 0.52] |
| Time_of_day:UR_c | 1.72 | [1.59, 1.88] | 1.31 | 0.58 | [0.53, 0.63] |
| Time_of_day:WBGT_c | 1.70 | [1.57, 1.86] | 1.30 | 0.59 | [0.54, 0.64] |

**Supplementary Table 21:** Results of the multicollinearity diagnosis for model 5 and and the outcome variable Low intensity distance covered per minute. Variance Inflation Factor (VIF), Increased Standard Error, and Tolerance values for each predictor in the model. These metrics assess the degree of multicollinearity among the continuous predictor variables. VIF > 10 indicates high multicollinearity and VIF > 5 indicates moderate multicollinearity.


**Fig S25: Histogram and Q-Q Plot of residuals; scatterplot residuals x fitted. Graphical analysis of normality and homoscedasticity of residuals**

<img src="images/FigS25-Low-intensity-model5-residuals-check.png" width="800" alt="Fig S25">

**Supplementary Figure 25:** Graphical analysis of the model residuals for assumptions assessment. The histogram and Q-Q plot were used to visually assess the normality of the residuals. The scatterplot of residuals versus fitted values was used to assess the assumption of homoscedasticity.

**Fig S26: Histogram and Q-Q Plot of random effects**

<img src="images/FigS26-Low-intensity-model5-random-effects-check.png" width="800" alt="Fig S26">

**Supplementary Figure 26**: Graphical assessment of the normality of the random effects. The histograms and Q-Q plots for each random effect are used to visually confirm the assumption that they are normally distributed.

**Table S22: Kolmogorov-Smirnov test for residuals and random effects normality check**
|Data| D | p-value|
|:--:|:--:|:-----:|
|Residuals|0.02|0.3|
|Random effects|0.04|0.08|

**Supplementary Table 22:** Kolmogorov-Smirnov test results to check the assumption of normality for both the model residuals and the random effects. The table shows the D statistic and the p-value for each test.

### Total distance covered per minute
**Table S23. Multicollinearity diagnosis**
|Predictor | VIF | VIF 95% CI | Increased SE | Tolerance | Tolerance 95% CI|
|:-----:|:-----:|:-------:|:--------------:|:-----------:|:-----------------:|
|Stage| 1.43| [1.33, 1.55]|         1.19|      0.70|     [0.64, 0.75]|
|Time_of_day |1.36 |[1.27, 1.48]|         1.17|      0.74|     [0.68, 0.79]|
|Ranking_difference |1.19| [1.12, 1.29]|         1.09|      0.84|     [0.78, 0.89]|
|Player_position |1.02 |[1.00, 1.45]|         1.01|      0.98|     [0.69, 1.00]|
|Player_age_c |1.04 |[1.01, 1.20]|         1.02|      0.96|     [0.83, 0.99]|
|Origin_climate |1.05 |[1.01, 1.19]|         1.02|      0.96|     [0.84, 0.99]|
|WBGT_c |2.10 |[1.93, 2.31]|         1.45|      0.48|     [0.43, 0.52]|
|UR_c| 2.12| [1.94, 2.32]|         1.45|      0.47|     [0.43, 0.52]|
|Time_of_day:UR_c |1.70| [1.57, 1.86]|         1.30|      0.59|     [0.54, 0.64]|
|Time_of_day:WBGT_c |1.69 |[1.56, 1.84]|         1.30|      0.59|     [0.54, 0.64]|

**Supplementary Table 23:** Results of the multicollinearity diagnosis for model 5 and and the outcome variable Total distance covered per minute. Variance Inflation Factor (VIF), Increased Standard Error, and Tolerance values for each predictor in the model. These metrics assess the degree of multicollinearity among the continuous predictor variables. VIF > 10 indicates high multicollinearity and VIF > 5 indicates moderate multicollinearity.

**Fig S27: Histogram and Q-Q Plot of residuals; scatterplot residuals x fitted. Graphical analysis of normality and homoscedasticity of residuals**

<img src="images/FigS27-Total-distance-model5-residuals-check.png" width="800" alt="Fig S27">

**Supplementary Figure 27:** Graphical analysis of the model residuals for assumptions assessment. The histogram and Q-Q plot were used to visually assess the normality of the residuals. The scatterplot of residuals versus fitted values was used to assess the assumption of homoscedasticity.

**Fig S28: Histogram and Q-Q Plot of random effects**

<img src="images/FigS28-Total-distance-model5-random-effects-check.png" width="800" alt="Fig S28">

**Supplementary Figure 28**: Graphical assessment of the normality of the random effects. The histograms and Q-Q plots for each random effect are used to visually confirm the assumption that they are normally distributed.

**Table S24: Kolmogorov-Smirnov test for residuals and random effects normality check**
|Data| D | p-value|
|:--:|:--:|:-----:|
|Residuals|0.03|0.06|
|Random effects|0.02|0.9|

**Supplementary Table 24:** Kolmogorov-Smirnov test results to check the assumption of normality for both the model residuals and the random effects. The table shows the D statistic and the p-value for each test.


## Licença

Este projeto está sob a licença MIT. Veja o arquivo LICENSE para mais detalhes.

---

Dúvidas ou sugestões? Abra uma issue ou envie um pull request!

LAFISE - Laboratório de Fisiologia do exercício - UFMG
