# Diagnostico de Doencas Cardiovasculares com Machine Learning

Projeto de Ciencia de Dados e Machine Learning focado em analise exploratoria de dados clinicos e classificacao preditiva para triagem de doencas cardiovasculares, utilizando a base historica da Cleveland Clinic Foundation (UCI Machine Learning Repository) e dados epidemiologicos do Brasil.

---

## Contexto e Objetivo

As doencas cardiovasculares representam a principal causa de mortalidade global. O objetivo deste projeto e identificar padroes clinicos associados a presenca de doenca cardiaca e construir um pipeline de classificacao supervisionada capaz de auxiliar na triagem de pacientes com alta sensibilidade (*Recall*), reduzindo o risco de falsos negativos.

---

## Estrutura do Repositorio

- `cardiovascular_disease_ml.ipynb`: Notebook Jupyter executado contendo analise exploratoria inicial e avancada, estatisticas estratificadas por diagnostico, visualizacoes clinicas e benchmark de classificadores.
- `.gitignore`: Configuracao de arquivos ignorados no versionamento.

---

## Analise Exploratoria e Achados Clinicos

Alem da avaliacao de idade, sexo, colesterol e serie historica de mortalidade no Brasil, a analise aprofundou quatro atributos clinicos essenciais:

- **Frequencia Cardiaca Maxima (`thalach`):** Pacientes com diagnostico positivo atingiram frequencia maxima significativamente menor (media de **139,26 bpm** e mediana de **142,00 bpm**) em comparacao ao grupo sem doenca (media de **158,38 bpm** e mediana de **161,00 bpm**).
- **Depressao do Segmento ST (`oldpeak`):** O grupo positivo apresentou mediana de **1,40** contra **0,20** no grupo negativo, consolidando-se como um forte marcador discriminativo.
- **Tipo de Dor Toracica (`cp`):** A categoria 4 (*Assintomatica*) concentrou **47,52%** da base total (144 pacientes) e registrou uma taxa de positividade de **72,92%** (105 casos positivos).
- **Pressao Arterial em Repouso (`trestbps`):** Mediana geral de **130,00 mm Hg**, com media de **134,57 mm Hg** no grupo positivo versus **129,25 mm Hg** no grupo negativo.

Todas as visualizacoes foram selecionadas seguindo as diretrizes do fluxograma *Chart Suggestions - A Thought-Starter* (Andrew Abela): boxplots comparativos para distribuicoes entre grupos, graficos de barras agrupadas para comparacao categorica e grafico de dispersao para relacoes bivariadas.

---

## Metodologia e Benchmark de Classificadores

Para garantir avaliacao imparcial e livre de vazamento de dados (*data leakage*), o conjunto de dados (303 registros e 13 variaveis preditoras) foi dividido de forma estratificada em **75% para treinamento** e **25% para teste**, aplicando `StandardScaler` dentro de um `Pipeline` ajustado exclusivamente sobre os dados de treino.

### Resultados na Base de Teste (25%)

| Modelo | Acuracia | Precision (Classe 1) | Recall (Classe 1) | F1-Score (Classe 1) | ROC-AUC |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Regressao Logistica** | **0.8684 (86.84%)** | **0.8378** | **0.8857** | **0.8611** | **0.9310** |
| **SVM (Kernel RBF)** | 0.8421 (84.21%) | 0.8108 | 0.8571 | 0.8333 | 0.9282 |
| **Gradient Boosting** | 0.8158 (81.58%) | 0.7692 | 0.8571 | 0.8108 | 0.9059 |

A **Regressao Logistica** apresentou o melhor desempenho geral, atingindo **86,84% de acuracia**, **88,57% de Recall** (identificando 31 dos 35 casos positivos no conjunto de teste) e **0,9310 de ROC-AUC**, aliando poder discriminativo e interpretabilidade clinica.

---

## Tecnologias Utilizadas

- **Linguagem:** Python 3.12
- **Manipulacao de Dados:** `pandas`, `numpy`
- **Visualizacao de Dados:** `matplotlib`, `seaborn`
- **Machine Learning:** `scikit-learn` (`Pipeline`, `StandardScaler`, `LogisticRegression`, `SVC`, `GradientBoostingClassifier`, `RandomForestClassifier`)
- **Ambiente:** Jupyter Notebook

---

## Como Executar Localmente

1. Clone o repositorio:
   ```bash
   git clone https://github.com/LuizSantiagojpg/cardiovascular-disease-ml.git
   cd cardiovascular-disease-ml
   ```
2. Instale as dependencias:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn jupyter
   ```
3. Abra e execute o notebook:
   ```bash
   jupyter notebook cardiovascular_disease_ml.ipynb
   ```
