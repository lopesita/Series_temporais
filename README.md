# Previsão de Demanda de Diesel no Estado de São Paulo

Este projeto apresenta um pipeline completo de Data Science para a previsão de consumo de combustível (**Diesel B**) no Estado de São Paulo. Utilizando dados históricos da **Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP)** provenientes da base `Liquidos_Venda_Atual`, o objetivo é projetar o volume de vendas combinando modelagem estatística clássica e algoritmos modernos de Machine Learning.

---

## 📌 Visão Geral do Projeto

A previsão de demanda de combustíveis é crucial para o planejamento logístico, refino e tomada de decisões estratégicas no setor de energia. Este projeto aborda o desafio através de duas vertentes principais:

1. **Abordagem Estatística:** Utilização do algoritmo **AutoARIMA** para capturar tendências e sazonalidades lineares intrínsecas da série temporal.
2. **Abordagem de Machine Learning:** Aplicação do **XGBoost Regressor**, estruturando o problema como um aprendizado supervisionado por meio da engenharia de atributos (*lag features* e variáveis de calendário).

### 🔍 Diferencial Técnico: Análise Contextual e Causalidade
O pipeline vai além da simples previsão, incluindo testes estatísticos rigorosos de estacionariedade (ADF) e a análise de **Causalidade de Granger** baseada em *lags* âncora, identificando relações de dependência temporal e a influência de preditores exógenos na demanda do estado de São Paulo.

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

1. **Carga e Filtragem:** Tratamento da base `Liquidos_Venda_Atual` focando no combustível Diesel B e na UF de São Paulo.
2. **Análise de Validação Estatística:** Aplicação do teste ADF para checar a necessidade de diferenciação da série e análise dos gráficos ACF/PACF.
3. **Decomposição da Série:** Isolamento dos componentes de sazonalidade anual e tendências de mercado.
4. **Modelagem Híbrida:** * Ajuste do benchmark estatístico via `auto_arima`.
   * Engenharia de recursos (criação de *lags* significativos validados via Granger) para alimentar o `XGBRegressor`.
5. **Avaliação:** Comparação fina de métricas de erro para determinar o modelo mais robusto para produção.

---

## 📊 Resultados e Conclusões

O projeto atingiu plenamente o objetivo de modelar e projetar a demanda de óleo diesel B em São Paulo para o ano de 2025, validando duas abordagens metodológicas complementares:

* **Machine Learning (XGBoost):** Otimizado via *Grid Search*, demonstrou robustez operacional ao explicar **77,64% da variância dos dados de teste ($R^2$)**, capturando interações não-lineares complexas a partir de lags âncora selecionados por Causalidade de Granger.
* **Estatística Clássica (Auto ARIMA):** Identificou autonomamente a arquitetura **SARIMAX(0,1,1)x(2,0,0)12**. A diferenciação ($d=1$) estabilizou a tendência ascendente de mercado, e os componentes sazonais exibiram máxima significância estatística ($p\text{-valor} < 0,001$) com resíduos classificados como ruído branco.

### 🧠 Principais Insights Analíticos

* **O Paradoxo da Otimização:** A imposição de restrições via *Grid Search* (benéfica ao XGBoost) causou um severo subajuste (*underfitting*) no ARIMA, achatando sua curva. A configuração *baseline* (heurística *stepwise*) mostrou-se amplamente superior, acompanhando com precisão os picos e vales reais de 2025.
* **Métricas de Excelência (ARIMA Baseline):** Alcançou um **MAPE de apenas 3,06%** (contra 7,13% da versão otimizada), apresentando um MAE de 35,44 e RMSE de 41,42 mil m³.
* **Complementaridade e Mitigação de Riscos:** O Auto ARIMA delimitou rigorosamente os intervalos de confiança probabilísticos, explicitando a incerteza ao longo do horizonte preditivo e mitigando o risco de extrapolação nativo das árvores de decisão do XGBoost.

### ⚠️ Limitações e Trabalhos Futuros

* **Limitação:** Sensibilidade e latência dos modelos univariados frente a choques macroeconômicos atípicos de curto prazo (como o descasamento registrado especificamente no mês de junho), que superam a inércia estatística da série histórica.
* **Próximos Passos:** 1. Incorporação de variáveis exógenas diretas (indicadores de atividade industrial e índices de preços de combustíveis).
  2. Implementação de arquiteturas híbridas unindo o aprendizado complexo do XGBoost ao rigor probabilístico dos resíduos do ARIMA.
  3. Expansão do horizonte preditivo para fornecer subsídios quantitativos sólidos para o planejamento de longo prazo da infraestrutura energética nacional.

---

## 👥 Autores

Trabalho desenvolvido em colaboração por:
* **Gabriel Chaves Gonçalves**
* **Ítalo Lopes** 
