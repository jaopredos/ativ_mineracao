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
| **Sopro** | 9.0% | **Crítico.** 34.42% dos pacientes possuem sopro. | ⭐⭐⭐ Alta |
| **Pulsos** | 9.0% | Requer tratamento de nulos. | ⭐⭐ Média/Alta |
| **FC** (Freq. Cardíaca) | 14.5% | Dado vital importante. | ⭐⭐ Média |
| **Peso** | 2.5% | Contém ruídos graves (Ex: valores negativos como `-40`). | ⭐ Baixa/Média |
| **Altura** | 0.0% | Dados completos, mas verificar consistência. | ⭐ Baixa/Média |
| **Idade** | 11.5% | Contém ruídos graves (Ex: `-113.18`, `0.01`). Essencial para *Feature Engineering*. | ⭐ Média (Indireta) |
| **IMC** | 36.0% | Alto índice de faltantes. Validar com tabelas de crescimento. | ❓ A verificar |
| **Motivo 1** | 8.2% | Texto livre ou categórico? | ❓ A verificar |
| **Motivo 2** | 27.0% | Alta ausência. | 🔻 Baixa |
| **Convênio** | 32.0% | Dado administrativo. | 🔻 Baixa |
| **HDA 1** | 33.0% | Histórico da Doença Atual. | ⭐ Média |
| **HDA 2** | 97.0% | **Candidata a exclusão** (quase vazia). | ❌ Nula |
| **Atendimento / DN** | 7.5% - 11% | Datas. Úteis apenas para cálculo de idade ou sazonalidade. | 🔻 Baixa (Direta) |
| **ID** | 0.0% | Identificador único. **Excluir da modelagem.** | ❌ Nula |
| **B2** | 9.0% | Tipo de som cardíaco. | ⭐ Média/Alta |

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