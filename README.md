# Previsão de Demanda de Diesel no Estado de São Paulo

Este projeto apresenta um pipeline completo de Data Science para a previsão de consumo de combustível (**Diesel**) no Estado de São Paulo. Utilizando dados históricos da **Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP)** provenientes da base `Liquidos_Venda_Atual`, o objetivo é projetar o volume de vendas combinando modelagem estatística clássica e algoritmos modernos de Machine Learning.

---

## 📌 Visão Geral do Projeto

A previsão de demanda de combustíveis é crucial para o planejamento logístico, refino e tomada de decisões estratégicas no setor de energia. Este projeto aborda o desafio através de duas vertentes principais:

1. **Abordagem Estatística:** Utilização do algoritmo **AutoARIMA** para capturar tendências e sazonalidades lineares intrínsecas da série temporal.
2. **Abordagem de Machine Learning:** Aplicação do **XGBoost Regressor**, estruturando o problema como um aprendizado supervisionado por meio da engenharia de atributos (*lag features* e variáveis de calendário).

### 🔍 Diferencial Técnico: Análise Contextual e Causalidade
O pipeline vai além da simples previsão, incorporando testes estatísticos rigorosos de estacionariedade (ADF) e a análise de **Causalidade de Granger**, identificando relações de dependência temporal e a influência de preditores exógenos na demanda do estado de São Paulo.

---

## 🛠️ Tecnologias e Dependências

O projeto foi desenvolvido em **Python** utilizando o ambiente **Google Colab**. Abaixo estão as principais bibliotecas utilizadas, divididas por contexto de aplicação:

### Manipulação e Visualização de Dados
* `pandas` & `numpy` — Processamento e estruturação dos dados tabulares da ANP.
* `matplotlib` & `seaborn` — Geração de gráficos analíticos e plotagem de séries temporais.

### Análise Estatística de Séries Temporais (`statsmodels` & `pmdarima`)
* `seasonal_decompose` — Decomposição analítica da série em Tendência, Sazonalidade e Resíduo.
* `plot_acf` & `plot_pacf` — Análise de autocorrelação para identificação de termos autorregressivos e de média móvel.
* `adfuller` — Teste de Dickey-Fuller Aumentado (ADF) para verificação de estacionariedade.
* `grangercausalitytests` — Teste de Causalidade de Granger para avaliar precedência temporal entre variáveis.
* `auto_arima` — Seleção automatizada dos melhores hiperparâmetros para o modelo ARIMA/SARIMA.

### Machine Learning e Avaliação (`scikit-learn` & `xgboost`)
* `XGBRegressor` — Modelo de árvore de decisão com gradient boosting para captura de relações não-lineares complexas.
* `mean_absolute_error`, `mean_squared_error`, `r2_score` — Métricas de validação matemática do erro dos modelos (MAE, RMSE e $R^2$).

---

## 🚀 Estrutura do Pipeline

1. **Carga e Filtragem:** Tratamento da base `Liquidos_Venda_Atual` focando no combustível Diesel e na UF de São Paulo.
2. **Análise de Validação Estatística:** Aplicação do teste ADF para checar a necessidade de diferenciação da série e análise dos gráficos ACF/PACF.
3. **Decomposição da Série:** Isolamento dos componentes de sazonalidade anual e tendências macroeconômicas.
4. **Modelagem Híbrida:** * Ajuste do benchmark estatístico via `auto_arima`.
   * Engenharia de recursos (criação de *lags* significativos validados via Granger) para alimentar o `XGBRegressor`.
5. **Avaliação:** Comparação fina de métricas de erro para determinar o modelo mais robusto para produção.

---

## 📊 Resultados

Os modelos demonstraram alta aderência histórica, provando que a flexibilidade do XGBoost combinada com o rigor estatístico do AutoARIMA oferece uma ferramenta confiável para mitigação de riscos e planejamento de estoque de combustíveis.

---
Desenvolvido por [Gabriel Chaves Gonçalves](https://github.com/seu-usuario)
