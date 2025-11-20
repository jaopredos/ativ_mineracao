# 📊 Relatório de Análise Exploratória Inicial (EDA)

## 1. Visão Geral do Dataset
* **Volume de Dados:** 12.873 registros.
* **Dimensionalidade:** 20 variáveis (features).
* **Tipagem:** 13 variáveis categóricas e 7 numéricas.

## 2. Análise da Variável Alvo (*Target*)
A variável `NORMAL X ANORMAL` apresenta o seguinte comportamento:
* **Distribuição de Classes:**
    * 🟢 **Normal:** 57.62%
    * 🔴 **Anormal:** 42.38%
* **Qualidade:** 9% dos registros não possuem rótulo (dados faltantes).
    * *Ação recomendada:* Avaliar se estes 9% devem ser descartados ou se há padrão na ausência do rótulo.

## 3. Dicionário de Dados e Qualidade (Data Quality)

Abaixo, detalhamos a integridade e a utilidade esperada de cada variável para o modelo de KDD.

### Tabela de Variáveis e Dados Faltantes

| Variável | % Faltante (aprox.) | Status / Observação | Potencial Preditivo |
| :--- | :---: | :--- | :---: |
| **Sopro** | 9.0% | **Crítico.** 34.42% dos pacientes possuem sopro. Forte indício de anomalia. | ⭐⭐⭐ Alta |
| **PPA** | 1.7% | **Feature Chave.** Variável derivada (normalizada por idade/sexo). Baixa ausência torna-a superior à PAS/PAD brutas. | ⭐⭐⭐ Alta |
| **Pulsos** | 9.0% | Requer tratamento de nulos. Indicador vital físico. | ⭐⭐ Média/Alta |
| **B2** | 9.0% | Tipo do segundo som cardíaco (bulha). Relevante para ausculta. | ⭐⭐ Média/Alta |
| **FC** (Freq. Cardíaca) | 14.5% | Dado vital importante. Verificar outliers. | ⭐⭐ Média |
| **SEXO** | 0.03% | Fundamental para cálculos de referência (ex: curvas de crescimento e pressão). | ⭐⭐ Média (Essencial) |
| **HDA 1** | 33.0% | Histórico da Doença Atual. Pode conter palavras-chave valiosas. | ⭐ Média |
| **Idade** | 11.5% | Contém ruídos graves (Ex: `-113.18`). Essencial para categorização do paciente. | ⭐ Média (Indireta) |
| **Peso** | 2.5% | Contém ruídos (valores negativos). Base para cálculo de IMC. | ⭐ Baixa/Média |
| **Altura** | 0.0% | Dados completos. Base para cálculo de IMC. | ⭐ Baixa/Média |
| **IMC** | 36.0% | Alto índice de faltantes. Necessário recalcular usando Peso/Altura para recuperar dados. | ❓ A verificar |
| **PAS** (Sistólica) | 60.0% | **Alta Ausência.** Provavelmente substituída pela variável `PPA`. | 🔻 Baixa (Usar PPA) |
| **PAD** (Diastólica) | 60.0% | **Alta Ausência.** Provavelmente substituída pela variável `PPA`. | 🔻 Baixa (Usar PPA) |
| **Motivo 1** | 8.2% | Texto livre ou categórico. Requer NLP ou limpeza. | ❓ A verificar |
| **Motivo 2** | 27.0% | Alta ausência. Informação complementar rara. | 🔻 Baixa |
| **Convênio** | 32.0% | Dado administrativo/financeiro. Baixa relevância clínica. | 🔻 Baixa |
| **Atendimento / DN** | 7.5% - 11% | Úteis apenas para engenharia de features (cálculo de idade exata). | 🔻 Baixa (Direta) |
| **HDA 2** | 97.0% | **Candidata a exclusão** (virtualmente vazia). | ❌ Nula |
| **ID** | 0.0% | Identificador único. **Excluir da modelagem.** | ❌ Nula |


## 4. Anomalias e Ruídos Identificados
Durante a inspeção inicial, foram detectados valores fora do domínio possível (*outliers* ou erros de digitação) que necessitam de limpeza antes da etapa de modelagem:
* **Peso:** Presença de valores negativos (ex: `-40 kg`).
* **Idade:** Valores inconsistentes (ex: `-113.18` anos, `0.01` anos).
* **Sexo:** 11.04% dos registros constam como "Indeterminado". Necessário investigar se é erro de coleta ou categoria válida para recém-nascidos intersexo/ambíguos.

## 5. Principais Insights e Hipóteses

1.  **O Poder do "Sopro":**
    * A variável `Sopro` desponta como a *feature* mais determinante até o momento.
    * **Estatística Chave:** Em 95.68% dos casos onde há presença de sopro, o diagnóstico final é **ANORMAL**. Isso sugere uma correlação fortíssima com a variável alvo.

2.  **Demografia (Sexo):**
    * Predominância masculina na base: 52.26% Masculino vs 36.70% Feminino.
    * *Hipótese:* Investigar se patologias cardíacas nesta região/amostra afetam mais meninos, ou se há um viés na coleta (ex: meninos sendo levados ao médico com mais frequência).

3.  **Feature Engineering (Próximos Passos):**
    * As variáveis `Peso` e `Altura` sozinhas podem ser fracas, mas são fundamentais para recalcular o `IMC` (que tem 36% de nulos) e validar os dados existentes.
    * As datas (`DN` e `Atendimento`) devem ser usadas para recalcular a `Idade` exata e corrigir os ruídos (valores negativos) encontrados nessa coluna.