# 🚗⚡ Análise e Modelagem de Padrões de Carregamento de Veículos Elétricos

## 📋 Sobre o Projeto

Este projeto tem como objetivo realizar uma análise estatística e aplicar técnicas de **Machine Learning** para compreender os padrões de carregamento de veículos elétricos.

A análise utiliza dados relacionados ao consumo de energia e à taxa de carregamento, permitindo explorar o comportamento das variáveis por meio de conceitos de **Estatística**, **Distribuição Normal** e **Regressão Linear**.

O projeto foi desenvolvido como parte das atividades acadêmicas da **Sprint 3 – Machine Learning e Análise de Dados**.

---

## 🎯 Objetivos

Os principais objetivos do projeto são:

* 📊 Analisar os dados de **energia consumida durante o carregamento**;
* ⚡ Avaliar a variável relacionada à **taxa de carregamento**;
* 📈 Calcular medidas estatísticas importantes, como média, mediana e desvio padrão;
* 🎲 Estimar probabilidades utilizando a **Distribuição Normal**;
* 🤖 Desenvolver um modelo de **Regressão Linear**;
* 🔎 Analisar a relação entre a taxa de carregamento e a energia consumida;
* 📉 Visualizar os resultados por meio de gráficos.

---

# 🛠️ Tecnologias e Bibliotecas Utilizadas

O projeto foi desenvolvido utilizando a linguagem **Python** e as seguintes bibliotecas:

| Tecnologia      | Finalidade                                  |
| --------------- | ------------------------------------------- |
| 🐍 Python       | Linguagem principal do projeto              |
| 🔢 NumPy        | Operações numéricas e estatísticas          |
| 🐼 Pandas       | Manipulação e análise dos dados             |
| 📊 Matplotlib   | Criação de gráficos                         |
| 🎨 Seaborn      | Visualização de dados                       |
| 📐 SciPy        | Cálculos relacionados à Distribuição Normal |
| 🤖 Scikit-learn | Implementação do modelo de Regressão Linear |

---

# 📂 Estrutura do Projeto

```text
📁 Projeto
│
├── 📓 SPRINT3_MLAM_2SEMESTRE.ipynb
│
├── 📊 Dataset
│   └── ev_charging_patterns_orange.csv
│
└── 📄 README.md
```

---

# 📊 Dataset

O projeto utiliza um conjunto de dados contendo informações relacionadas ao carregamento de veículos elétricos.

Entre as principais variáveis analisadas estão:

### ⚡ Energia Consumida

Representa a quantidade de energia consumida durante o processo de carregamento, medida em:

```text
kWh (quilowatt-hora)
```

No código, essa variável é utilizada com o nome:

```python
Energia_Consumida
```

### 🔌 Taxa de Carregamento

Representa a potência ou velocidade associada ao carregamento do veículo elétrico, medida em:

```text
kW (quilowatt)
```

No código, essa variável é utilizada com o nome:

```python
Taxa_Carregamento
```

---

# 🔄 Etapas da Análise

## 1️⃣ Importação das Bibliotecas

Inicialmente, são importadas as bibliotecas necessárias para:

* Manipulação de dados;
* Cálculos estatísticos;
* Visualização gráfica;
* Modelagem de Machine Learning.

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from scipy.stats import norm
from sklearn.linear_model import LinearRegression
```

Também é configurado um tema visual para melhorar a apresentação dos gráficos.

---

# 2️⃣ Carregamento e Preparação dos Dados

Os dados são carregados a partir de um arquivo CSV utilizando a biblioteca **Pandas**.

```python
df = pd.read_csv('/content/ev_charging_patterns_orange.csv')
```

Posteriormente, algumas colunas recebem nomes mais simples e adequados para utilização durante a análise:

```python
df.rename(
    columns={
        'Energy Consumed (kWh)': 'Energia_Consumida',
        'Charging Rate (kW)': 'Taxa_Carregamento'
    },
    inplace=True
)
```

---

# 📐 3️⃣ Análise Estatística

A análise estatística é realizada principalmente sobre a variável:

> **Energia Consumida**

São calculados indicadores importantes, como:

* 📊 Média;
* 📉 Mediana;
* 📏 Desvio padrão.

Essas métricas permitem compreender a distribuição e a variabilidade dos dados relacionados ao consumo energético dos veículos.

---

# 🎲 4️⃣ Cálculo de Probabilidades

O projeto utiliza a **Distribuição Normal** para estimar probabilidades relacionadas à energia consumida durante os processos de carregamento.

---

## 🔹 Probabilidade Acima da Mediana

Inicialmente, é calculada a mediana da energia consumida.

Em seguida, é estimada a probabilidade de um determinado carregamento apresentar um consumo superior a esse valor.

A probabilidade é calculada utilizando:

```python
norm.sf()
```

A função representa a probabilidade acumulada acima de determinado valor.

---

## 🔹 Classificação dos Eventos

O projeto também implementa uma classificação para interpretar as probabilidades obtidas.

Os eventos podem ser classificados como:

| Probabilidade   | Classificação     |
| --------------- | ----------------- |
| Menor que 5%    | 🔴 Raro           |
| Entre 5% e 50%  | 🟠 Pouco provável |
| Entre 50% e 95% | 🟢 Provável       |
| Superior a 95%  | 🔵 Quase certo    |

Essa classificação facilita a interpretação dos resultados estatísticos.

---

# 📊 5️⃣ Probabilidade no Intervalo Média ± 2 Desvios Padrão

Também é analisada a probabilidade de os valores estarem dentro do intervalo:

```text
Média ± 2 × Desvio Padrão
```

Matematicamente:

```text
Limite Inferior = Média - 2s
Limite Superior = Média + 2s
```

Onde:

```text
s = Desvio Padrão
```

A probabilidade é calculada utilizando a diferença entre as funções de distribuição acumulada:

```python
norm.cdf(limite_superior) - norm.cdf(limite_inferior)
```

Essa análise permite verificar a concentração dos valores de energia consumida em torno da média.

---

# 🤖 6️⃣ Modelagem com Regressão Linear

O projeto implementa um modelo de **Regressão Linear** para analisar a relação entre:

### Variável Independente

```text
Taxa de Carregamento
```

### Variável Dependente

```text
Energia Consumida
```

A implementação utiliza a biblioteca **Scikit-learn**.

```python
modelo = LinearRegression()
modelo.fit(X, y)
```

O modelo busca identificar uma relação matemática entre as variáveis por meio da equação:

```text
y = β₁x + β₀
```

Onde:

* **y** → Energia Consumida;
* **x** → Taxa de Carregamento;
* **β₁** → Coeficiente angular;
* **β₀** → Intercepto.

---

# 📈 7️⃣ Visualização dos Dados

Para facilitar a interpretação dos resultados, é gerado um gráfico contendo:

* 🔵 Os dados reais do dataset;
* 📈 A reta estimada pelo modelo de Regressão Linear.

O gráfico permite visualizar a relação entre:

```text
Taxa de Carregamento × Energia Consumida
```

A visualização é construída utilizando:

* **Matplotlib**
* **Seaborn**

---

# 📌 Principais Conceitos Aplicados

Durante o desenvolvimento do projeto, foram utilizados conceitos importantes de Estatística e Machine Learning.

### 📊 Estatística

* Média;
* Mediana;
* Desvio padrão;
* Probabilidade;
* Distribuição Normal;
* Função de distribuição acumulada.

### 🤖 Machine Learning

* Regressão Linear;
* Variáveis independentes e dependentes;
* Treinamento de modelo;
* Coeficiente angular;
* Intercepto;
* Predição de valores.

---

# 🔎 Conclusões

A análise permite compreender o comportamento da **energia consumida durante o carregamento de veículos elétricos** e investigar sua relação com a **taxa de carregamento**.

A utilização de ferramentas estatísticas possibilita analisar:

* A tendência central dos dados;
* A dispersão dos valores;
* A probabilidade de determinados eventos;
* A concentração dos dados em torno da média.

Além disso, a aplicação da **Regressão Linear** permite construir um modelo capaz de representar matematicamente a relação entre a taxa de carregamento e a energia consumida.

Dessa forma, o projeto demonstra como técnicas de **Análise de Dados, Estatística e Machine Learning** podem ser aplicadas ao contexto da mobilidade elétrica e da infraestrutura de carregamento de veículos elétricos. 🚗⚡

---

# ▶️ Como Executar o Projeto

## 1. Clone o repositório

```bash
git clone <URL_DO_REPOSITORIO>
```

## 2. Instale as dependências necessárias

```bash
pip install numpy pandas matplotlib seaborn scipy scikit-learn
```

## 3. Abra o notebook

O projeto pode ser executado utilizando:

* 📓 Jupyter Notebook;
* ☁️ Google Colab;
* 💻 Visual Studio Code.

Abra o arquivo:

```text
SPRINT3_MLAM_2SEMESTRE.ipynb
```

---

# 🏫 Contexto Acadêmico

Projeto desenvolvido para fins acadêmicos, com foco na aplicação prática de conceitos de:

> **Machine Learning • Estatística • Análise de Dados • Python**

---

<div align="center">

### 🚗⚡ Análise de Dados para uma Mobilidade Mais Inteligente e Sustentável ⚡🚗

</div>
