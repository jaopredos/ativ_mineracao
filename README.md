# Predição de Condição Cardíaca em Crianças e Adolescentes

Este repositório documenta o processo de **Knowledge Discovery in Databases (KDD)** aplicado a um conjunto de dados médicos reais. O objetivo é identificar padrões e predizer a presença de patologias cardíacas em pacientes pediátricos.

## 📄 Sobre o Projeto

Muitas vezes assume-se erroneamente que crianças possuem corações saudáveis, o que permite que doenças evoluam de forma silenciosa até que seja tarde demais para um tratamento preventivo. No Brasil, estima-se que entre 8 e 10 crianças a cada 1.000 nascem com alguma doença cardíaca congênita. Fatores de risco modernos, como obesidade e sedentarismo em jovens, agravam este cenário.

O objetivo principal deste trabalho é aplicar o processo de KDD para predição e extração de conhecimento de patologias cardíacas em crianças e jovens (0 a 19 anos).

## 📊 Fonte dos Dados

Os dados utilizados neste estudo foram coletados no **Real Hospital Português (RHP)** em Recife-PE, Brasil.
* **Ética:** Os dados foram anonimizados e sua utilização aprovada pelo Comitê de Ética do RHP e pelo Comitê de Ética da Universidade do Porto, Portugal.
* **População:** Crianças e jovens entre 0 e 19 anos.
* **Target:** Variável `NORMAL X ANORMAL` (Presença ou ausência de patologia).

## 📂 Dicionário de Dados

Abaixo estão listadas as variáveis presentes no dataset:

| Variável | Descrição |
| :--- | :--- |
| **ID** | ID do paciente anônimo |
| **Peso** | Peso do paciente (kg) |
| **Altura** | Altura do paciente (m) |
| **IMC** | Índice de Massa Corporal |
| **Atendimento** | Data da visita médica |
| **DN** | Data de nascimento |
| **IDADE** | Idade do paciente |
| **Convenio** | Tipo de seguro de saúde |
| **PULSOS** | Pulsação |
| **PA SISTOLICA** | Pressão Arterial Sistólica (PAS) |
| **PA DIASTOLICA** | Pressão Arterial Diastólica (PAD) |
| **PPA** | Resultado PAS/PAD (Cálculo baseado em tabelas clínicas) |
| **NORMAL X ANORMAL** | **Variável Alvo**: Ausência ou presença de patologia |
| **B2** | Tipo do segundo som cardíaco |
| **SOPRO** | Tipo de sopro cardíaco |
| **FC** | Frequência Cardíaca |
| **HDA 1** | Histórico da doença 1 |
| **HDA2** | Histórico da doença 2 |
| **SEXO** | Sexo do paciente |
| **MOTIVO1** | Motivo primário do encaminhamento |
| **MOTIVO2** | Motivo secundário do encaminhamento |

> **Nota Técnica:** Para o enriquecimento da análise (Etapa de Transformação), estão sendo consultadas tabelas externas de cardiologia pediátrica para validar intervalos de referência para **IDADE** e **IMC**.

## 🚀 Etapas do Projeto (KDD)

Este repositório está organizado conforme a evolução das etapas do KDD:

1.  **Seleção e Coleta:** Dados brutos extraídos dos sistemas do RHP.
2.  **Pré-processamento:** Limpeza de dados, tratamento de nulos e anonimização.
3.  **Transformação:** Normalização e criação de novas features (ex: categorização de IMC por idade).
4.  **Data Mining:** Aplicação de algoritmos de Machine Learning para classificação (Normal vs. Anormal).
5.  **Interpretação/Avaliação:** Análise das métricas (Acurácia, Recall, F1-Score) e validação clínica dos padrões encontrados.

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python 3.x
* **Bibliotecas Principais:** Pandas, Scikit-learn, Matplotlib/Seaborn, NumPy.
* **Ambiente:** Jupyter Notebooks.

## 📈 Status do Projeto

* [x] Coleta e entendimento dos dados
* [ ] Análise Exploratória (EDA)
* [ ] Tratamento de dados faltantes
* [ ] Modelagem Preditiva
* [ ] Avaliação de Resultados

## 🤝 Autor

João Pedro de Castro - ![jaopredos](https://github.com/jaopredos)