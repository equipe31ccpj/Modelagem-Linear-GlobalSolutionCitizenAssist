# Modelagem-Linear-GlobalSolutionSeniorWatt

# SeniorWatt AI — Análise Estatística e Preditiva do Consumo Energético Residencial na Terceira Idade

Projeto desenvolvido para a avaliação **Global Solution (2º Semestre) — Disciplina de MLAM**, inserido no contexto do desafio **CitizenTech**.

---

## Integrantes do Grupo
* **Pedro Henrique Neves** — RM: `[571382]`
* **Akin Alexandre Mendes Martins** — RM: `[572773]`
* **Maria Eduarda Rocha Benjamim** — RM: `[570554]`

---

## Apresentação do Problema e Objetivo
O aumento contínuo das tarifas de energia elétrica impacta diretamente o orçamento doméstico da população idosa, que frequentemente vive com renda fixa e passa mais tempo dentro de casa. Além do impacto financeiro, o conforto térmico (uso de climatização) é uma questão de bem-estar e saúde para esse público.

**Objetivo:** Coletar, tratar e analisar dados reais de consumo residencial utilizando estatística inferencial e modelos preditivos em Python para fundamentar o motor de inteligência do assistente digital **SeniorWatt AI**, capaz de alertar sobre picos de gasto, prever faturas e identificar equipamentos de alto impacto (como ar-condicionado).

---

## Descrição da Base de Dados
* **Nome:** *Household Energy Consumption* (Registros de 2025)
* **Fonte Original:** Kaggle — [Acesse a base original no Kaggle](https://kaggle.com) *(Nota: insira aqui o link exato da página do dataset no Kaggle)*
* **Volume Total:** 90.000 registros originais.
* **Recorte Amostral:** Foram filtradas **30.437 residências** compostas por **1 a 2 moradores** (`Household_Size <= 2`), adotado como perfil domiciliar representativo de lares da terceira idade (idosos que moram sozinhos ou em casal).
* **Principais Variáveis Analisadas:**
  * `Energy_Consumption_kWh`: Consumo total diário de energia elétrica (kWh).
  * `Peak_Hours_Usage_kWh`: Consumo registrado especificamente no horário de pico (kWh).
  * `Avg_Temperature_C`: Temperatura média ambiente (°C).
  * `Has_AC`: Variável categórica binária indicando a presença de ar-condicionado (`Yes` / `No`).

---

## Organização do Repositório
```text
├── household_energy_consumption.csv   # Base de dados utilizada nas análises
├── analise_mlam_seniorwatt.ipynb      # Notebook Python com cálculos, modelos e gráficos
├── Relatorio_Estatistico_MLAM.pdf     # Relatório técnico completo com interpretações
└── README.md                          # Documentação geral do projeto
```

---

## ⚙️ Bibliotecas e Execução do Código
Para reproduzir as análises localmente ou no **Google Colab**:
1. Certifique-se de que o arquivo `household_energy_consumption.csv` esteja no mesmo diretório (ou carregado na pasta `/content/` do Colab).
2. Instale as dependências necessárias caso execute localmente:
   ```bash
   pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn
   ```
3. Abra o notebook `.ipynb` e execute todas as células sequencialmente.

---

## 📈 Síntese dos Principais Resultados
* **Distribuição Normal:** O consumo médio diário no perfil sênior é de **4,76 kWh** (mediana de **4,60 kWh** e desvio padrão de **2,34 kWh**). A probabilidade de consumo acima da mediana é de **52,64%** (evento muito provável).
* **Testes de Hipóteses:** No Teste Z unilateral à esquerda ($n=20, \alpha=6\%$), rejeitou-se $H_0$ ($p = 0,0062$), mostrando que subgrupos específicos podem apresentar consumo significativamente inferior à média geral. No teste unilateral à direita ($n=25, \alpha=9\%$), não houve evidência estatística para rejeitar $H_0$ ($p = 0,1189$).
* **Regressão Linear Simples:** Existe uma correlação linear positiva fortíssima ($r = 0,9665$) entre o consumo no horário de pico e o consumo total diário ($R^2 = 0,9342$). Para um gasto de **2,5 kWh** no pico, estima-se um consumo total de **5,90 kWh/dia**.
* **Regressão Linear Múltipla:** A inclusão da temperatura média manteve o poder explicativo em **93,42%** ($R^2 = 0,9342$, Teste $F = 216.112,30$, $p < 0,0001$), projetando **5,94 kWh/dia** para pico de 2,5 kWh a 24°C.
* **Regressão Logística Binária:** O modelo classificou com **96,74% de acurácia** se a residência possui ar-condicionado a partir dos padrões de consumo e temperatura.

---

## ⚠️ Limitações Identificadas
* **Proxy Demográfico:** A base de dados não possui uma coluna explícita informando a idade dos moradores; utilizou-se o tamanho da família (`Household_Size <= 2`) como critério de aproximação para o perfil da terceira idade.
* **Ausência de Variáveis Socioeconômicas e Tarifárias:** O dataset registra o consumo físico em kWh, mas não contempla bandeiras tarifárias locais, renda domiciliar ou eficiência energética (selo Procel) de cada eletrodoméstico individualmente.
